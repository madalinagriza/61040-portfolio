# Concept Questions

1. **Contexts:** Contexts allow for identical nonces to be generated across different contexts. Uniqueness is therefore enforced in the context scope, and not globally across all contexts. For urlShortening, the domains will be contexts, therefore we can have a <ins>bit.ly/short</ins> link and a <ins>yellkey.com/short</ins> link. 

2. **Storing used strings:** Similarly, used strings should be stored per context. To generate unique nonces in a given context we need to remember already generated nonces. If a counter is used, we have the property that: the set of used strings in context x corresponds exactly to all ids <= c<sub>x</sub>, where c<sub>x</sub> is the counter per context. Abstraction function is:\
used<sub>x</sub> = { represent(i) | 0 <= i < c<sub>x</sub> }, where represent is the function used to map from integer to nonce.

3. **Words as nonces**\
Advantage: increased readability, memorability for the user + very easy to verbally share.\
Disadvantage: finite set of nonces; makes short link more guessable; users might guess or associate the meaning of the word nonce with the link, but the chosen word may be inappropriate to the content of the target link.\
Modification: 
    - *Add to state:* each Context has a Vocabulary with a set of words Strings
    - *Modify actions:*
        - generates nonces by picking from vocabulary (and not already used in this context)
    - *Add actions:* 
        - addWord(vocabulary: Vocabulary, newWord: String):\
        requires newWord not in vocabulary & vocabulary exists\
        effects: adds newWord in vocab
        - deleteWord(context: Context, word: String):\
        requires: context exists, word is in context.vocabulary, no context.used uses word\
        effects: removes word from context.vocabulary


# Synchronization Questions

1. **Partial matching:** For generating a nonce, the sync needs just the base for the function, whereas for registering the link, it needs for the base and the targetUrl.
2. **Omitting names:** 
    - We can't omit field names that are different than their type name because then we can't disambiguate between two fields which have the same type (e.g Strings)
    - We can't omit field types because they inform system's behavior and relations between actions/state fields.

3. **Inclusion of request:** setExpiry is a sync fired from the system itself (when the time runs out), so it has no interaction needed with the user to be started. In comparison, generate & register are at the request of the user to shortenUrl, communicated through HTTP in practice. 

4. **Fixed domain:** remove shortUrlBase as a parameter from Request.shortenUrl and call the two actions (NonceGeneration.generate & UrlShortening.register) with the hardcoded domain set.

5. **Adding a sync:** \
sync expire\
when: ExpiringResource.expireResource(): (resource: Resource)\
then: UrlShortening.delete (shortUrl: resource)

# Extending the design

1. **Designing concepts**

**concept:** LinkAccessCounter

**purpose:** keep track of number of Url accesses\
**principle:** when an URL is accessed, the counter for that link increases; the count can be viewed

**state:**
>a set of Counters with
>>a Url String\
  a count Integer

**actions:** 
> createForNew(url: String)
>> requires: \
effects: if no counter.url present for that url, create a counter associated with url and count = 0

> increment(url: String)
>> requires: counter exists associated with url\
effects: increments counter.count by 1

> read(url: String): (count: Integer)
>> requires: counter exists associated with url\
effects: returns counter.count

**concept:** AnalyticsAuth[User]\
**purpose:** restricts analytics access to the creator of the url\
**principle:** when a short URL is registered, its creator is recorded; the creator can view access analytics for all the ShortUrl they created\
**state:**
>a set of Permissions with
>> an url String\
a creator User

**actions:**

>registerCreator(url: String, creator: User)
>> requires: no existing permissions for this url\
effects: creates a permission associated with url and creator

>checkCreator(url: String, creator: User)
>> requires: permission with this url exists, and permission.creator is creator


2. **Syncs**

**sync** startCount\
**when** UrlShortening.register(shortUrlSuffix, shortUrlBase, targetUrl: string): (shortUrl: String)\
**then** LinkAccessCounter.createForNew(shortUrl: String)

**sync** incrementCount\
**when** UrlShortening.lookup(shortUrl:String)\
**then** LinkAccessCounter.increment(shortUrl: String)

**sync** viewAnalytics\
**when** Request.viewAnalytics(creator: User, shortUrl: String)\
**and**  AnalyticsAuth.checkCreator(creator, shortUrl) : (ok)\
**where** LinkAccessCounter.read(shortUrl: string): (count: Integer)\
**then** Response.returnAnalytics (shortUrl, count)

3. **Feature extensions:**
    - *Allowing users to choose their own short URLs:* extend register sync to take in a customAlias. UrlShortening already checks for alias uniqueness.
    - *Using the “word as nonce” strategy to generate more memorable short URLs:*
    Have a vocabulary of words that can be used, extract new nonces from that vocabulary.
    - *Including the target URL in analytics, so that lookups of different short URLs can be grouped together when they refer to the same target URL:*\
    Make a new concept which structures targetUrls by User, and maps to the collection of shortUrl; When the request is to search by targetUrl, a sync calls structureUrl.getAliases which returns a list of shortUrls. Another sync looks up the counts for every short link. 
    - *Generate short URLs that are not easily guessed:*\
    Add a new concept NonceStrength, which has a collection of rules to check when a custom nonce is given by the user. It can be related to the nonce length and/or randomness of letters/numbers. Add a new sync when user registers, that checks against these rules. Also, modify nonce generation ot directly generate hard to guess nonces.
    - *Supporting reporting of analytics to creators of short URLs who have not registered as user:*\
    Use tokens to share view permissions. Have a validate function, and then add a sync which calls validate token when checkCreator is called.

