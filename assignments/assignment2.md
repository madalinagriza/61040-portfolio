## Problem Domain: Personal Finance and Spending Awareness
Financial awareness is a vital life skill, yet it is rarely taught formally. Many people struggle to build consistent habits around tracking their spending: available tools are often too passive, leaving users disconnected from their daily choices, or too effortful, causing them to abandon the process. The domain of personal finance, and especially everyday expense tracking and budgeting, highlights this tension between ease of use and meaningful engagement. Furthermore, rarely are existing apps able to fit every person, leaving users to either overlook unique spending patterns or force their habits into rigid categories.  

## Problem: High Friction in Expense Tracking
Users want to understand where their money goes, but the process of logging expenses is often frustrating. On one side, fully automated apps hide the details and make it hard to reflect on individual purchases. On the other, manual spreadsheets demand so much effort that people abandon them quickly. The result is disengagement: people struggle to sustain tracking long enough to gain intuition about what counts as "a lot" or "a little" in different categories. The core problem is that expense tracking tools either under-engage or over-burden users, preventing them from building meaningful financial awareness.

## Stakeholders
- **User:** The main beneficiary, who wants a low-effort but engaging way to track spending and build financial awareness.  
- **Banks:** Provide the raw material for tracking through statements; users rely on this data to begin the process. As a secondary-effect, better tracking from the user's part means fewer disputes, fewer "surprise charges," and therefore less user disatisfactions with banks.
- **Merchants:** Indirectly affected because clear tracking reveals price patterns, influencing loyalty and comparisons.  
- **Roommates/Family:** Secondary stakeholders, since improved financial awareness can reduce tension around shared expenses and budgeting.  

## Evidence and Comparables

1. **Low Engagement with Tracking** ([Yahoo Finance Survey](https://finance.yahoo.com/news/survey-more-two-thirds-americans-011626600.html))  
   More than two-thirds of Americans do not regularly review their expenses, showing that the barrier to consistent tracking is widespread.  

2. **Budgeting Stress:** ([Reddit thread](https://www.reddit.com/r/budget/comments/1bnrpia/how_many_budgeters_find_it_stressinducing_is/))  
   Users describe budgeting, especially manual entry, as stressful and draining, reinforcing that high-effort approaches fail to engage.  

3. **Low Retention in Finance Apps:** ([Sendbird Report](https://sendbird.com/blog/app-retention-benchmarks-broken-down-by-industry))  
   Only 5.8% of users remain active in finance apps after 30 days, suggesting that current tools fail to maintain engagement over time.  

4. **Comparables: YNAB** ([You Need a Budget](https://www.ynab.com/pricing))  
   Who'd want to start budgeting by spending money on a budget app? YNAB emphasizes labeling every expense and is widely recommended, but its $15/month subscription makes it inaccessible to many regular people, showing demand for simpler, cheaper alternatives.   

5. **Gamification Boosts Retention** ([Vorecol Blog](https://blogs.vorecol.com/blog-evaluating-the-effectiveness-of-mobile-apps-for-financial-literacy-and-wellness-161457))  
   Research shows gamified apps achieve 34% higher retention, suggesting interactive and rewarding approaches could directly address the engagement gap.  


### Application Pitch: FlashFinance

**Motivation**  
Tired of spending based on vibes? Most people want to understand their money, but tracking often feels impossible to sustain. Apps that automate too much leave users detached, while spreadsheets demand so much effort that they are quickly abandoned. Even worse, they often misinterpret the data: grocery shopping for $200 on your credit card, and then paying off the credit bill looks like $400 spent, and lumping everything into "food" ignores the difference between essentials and splurges. These problems add friction and confusion, discouraging people from sticking with the process. FlashFinance addresses these gaps with a quick, secure, and interactive way to process expenses that keeps users engaged and aware.


**Features:**  

- **Quick-Pick Labeling**  
  No need for tedious manual entry. After uploading a bank statement, transactions appear one by one in a streamlined quick-pick interface. With a simple tap, users assign each purchase to a category. This makes every expense visible while keeping the process fast, helping users internalize what "a lot" or "a little" feels like.  

- **Custom Categories:**  
  Track spending in a way that fits your life. FlashFinance lets users create categories that reflect their own priorities—distinguishing "weekly groceries" from "takeout splurges," or "campus lunch" from "entertainment." Personalized categories give more meaningful insights and help identify where there’s room to cut back.  

- **Spending Feedback**  
  Get insights that stick. Once labeling is complete, FlashFinance shows clear summaries by category and highlights how current spending compares to your past habits. This feedback reinforces awareness without overwhelming charts, supporting reflection and more transparent conversations with roommates or family.  

**Impact:**  
By combining quick interaction, personal control, and immediate feedback, FlashFinance transforms a stressful chore into a lightweight daily ritual. Statements are uploaded securely and stay private to each user. The result is higher engagement, stronger financial intuition, and a clearer picture of where money is really going.

## Concepts
**concept:** User

**purpose:**  
establish a unique identity for each person and control access to app functionality so that data is isolated per account

**principle:**  
every action in the app executes in the context of a specific, authenticated user; identity is stable (via user_id) and ownership/authorization checks rely only on that identity, not on knowledge of other concepts

**state:**
> a set of Users with  
>> a user_id ID  
>> an email Email  
>> a name String  
>> a password_hash String  
>> a status {ACTIVE | INACTIVE}

**actions:**
> register(email: Email, name: String, password: String): (user: User)  
>> *requires:*  
email is not used by any existing user  
>> *effects:*  
creates a new user with a fresh user_id, password_hash derived from password, status ACTIVE; adds the user to Users; returns the created user

> authenticate(email: Email, password: String): (user: User)  
>> *requires:*  
there exists a user with the given email whose password_hash matches password and whose status is ACTIVE  
>> *effects:*  
returns that user

> deactivate(user_id: ID)  
>> *requires:*  
a user with user_id exists  
>> *effects:*  
sets the user's status to INACTIVE

> changePassword(user_id: ID, old_password: String, new_password: String): (ok: Boolean)  
>> *requires:*  
a user with user_id exists and old_password matches the stored password_hash  
>> *effects:*  
updates password_hash with new_password; returns true

**invariants:**
- email uniquely identifies a single user  
- user_id is unique and never reused  

---

**concept:** Transaction

**purpose:** represent each imported bank record that a user will label

**principle:** transactions are immutable financial records owned by a user; transactions start UNLABELED and gain meaning when linked to a category via a label

**state:**
> a set of Transactions with  
>> a tx_id ID  
>> an owner_id ID    
>> a date Date  
>> a merchant_text String  
>> an amount Money  
>> a status {UNLABELED | LABELED}

**actions:**
> importTransactions(owner_id: ID, rows: [CSVRows]): (txs: [Transactions])  
>> *requires:* owner exists; rows are well-formed; all amounts are positive  
>> *effects:* parses rows into Transactions owned by owner_id with status UNLABELED; generates new tx_ids for each transaaction; adds them to state; returns the created list  

> mark_labeled(tx_id: ID, requester_id: ID)  
>> *requires:*  
transaction tx_id exists; requester_id = transaction.owner_id  
>> *effects:*  
sets transaction.status to LABELED

**invariants:**
- each transaction has exactly one owner_id
- transaction.amount is positive
- status is {UNLABELED, LABELED}
- transactions are created only by parsing a bank statement
- after a transaction first becomes LABELED, it never returns to UNLABELED
- after import, transactions remain immutable records that can be labeled but not directly edited.

---

**concept:** Category

**purpose:** allow users to define and manage meaningful groupings of their transactions

**principle:** categories are user-defined and reusable; each user maintains an independent set referenced by labels

**state:**
> a set of Categories with  
>> a category_name String
>> a category_id ID  
>> an owner_id ID 
>> a name String  

**actions:**
> create(owner_id: ID, name: String): (category: Category)  
>> *requires:*  
user owner_id exists; for the same owner_id, no existing category with same name  
>> *effects:*  
generated a new category_id; creates and stores a category under owner_id associated with name; returns it

> rename(owner_id: ID, category: Category, new_name: String): (category: Category)  
>> *requires:*  
category exists and category.owner_id = owner_id; for the same owner_id, no existing category with same new_name  
>> *effects:*  
updates category.name to new_name; returns updated category

> delete(owner_id: ID, category: Category): (ok: Boolean)  
>> *requires:*  
category exists and category.owner_id = owner_id  
>> *effects:*  
if no current-period label references this category, removes it and returns true; otherwise leaves state unchanged and returns false

**invariants:**
- (owner_id, name) is unique among Categories
- category_id is unique for the same user
- categories cannot belong to multiple users

---

**concept:** Label

**purpose:** record the user’s assignment of a specific transaction to a specific category so that spending meaning is explicit and auditable

**principle:** a label ties exactly one transaction to exactly one category for its owner; creating or changing a label never alters the transaction’s imported data and preserves a traceable history of who assigned what and when

**state:**
> a set of Labels with  
>> a tx_id ID  
>> a category_id ID  
>> an user_id ID  
>> a created_at Timestamp

**actions:**
> apply(user_id: ID, tx_id: ID, category_id: ID): (label: Label)  
>> *requires:*  
transaction exists and transaction.owner_id = user_id;  
category exists and category.owner_id = user_id;  
no existing label for tx_id in Labels  
>> *effects:*  
creates a label associating tx_id to category_id with user_id and current timestamp; adds it; returns the label

> update(user_id: ID, tx_id: ID, new_category_id: ID): (label: Label)  
>> *requires:*  
a label for tx_id exists; transaction.owner_id = user_id;  
new_category_id exists and has owner_id = user_id  
>> *effects:*  
replaces the label's category_id with new_category_id; updates created_at to now; returns updated label

> remove(user_id: ID, tx_id: ID): (ok: Boolean)  
>> *requires:*  
a label for tx_id exists; transaction.owner_id = user_id  
>> *effects:*  
reassigns the transaction’s label to the user's built-in Trash category_id; transaction remains LABELED; returns true

**invariants:**
- at most one label per tx_id
- label.user_id = transaction.owner_id for the labeled transaction
- a label's category.owner_id = label.user_id


---

**concept:** FeedbackMetric

**purpose:** provide per-user, per-category aggregates of labeled transactions so spending activity can be summarized and compared across time periods

**principle:** a feedback metric is a derived summary; it reflects but never alters the underlying transactions, and its role is to provide insight through aggregation



**state:**
> a set of FeedbackMetrics with  
>> an owner_id ID  
>> a category_id ID  
>> a period Period  
>> a current_total Money  

**actions:**
> recompute_for_period(owner_id: ID, category_id: ID, period: Period): (metric: FeedbackMetric)  
>> *requires:*  
owner exists; category exists with Category(category_id).owner_id = owner_id  
>> *effects:*  
creates or updates the FeedbackMetric identified by (owner_id, category_id, period), setting current_total to the sum of amounts of labeled transactions; returns it  

**invariants:**
- (owner_id, category_id, period) uniquely identifies a FeedbackMetric  
- current_total is nonnegative  
- FeedbackMetric.owner_id = Category.owner_id  



## Syncs
**Request -> Syncs**

**sync:** uploadStatementCreatesTransactions  
**when** Request.uploadStatement(owner_id: ID, file_ref: FileRef)  
**where:** rows = parse(file_ref: FileRef): [CSVRows]  
**then** Transaction.importTransactions(owner_id: ID, rows: [CSVRows])

---

**sync:** labelTransaction  
**when** Request.label(user_id: ID, tx_id: ID, category_id: ID)  
**where:** Transaction.owner(tx_id: ID): ID = user_id  
**and** Category.owner(category_id: ID): ID = user_id  
**then** Label.apply(user_id: ID, tx_id: ID, category_id: ID)

---

**Intra-Concept Syncs**

**sync:** applyLabelSetsStatus  
**when** Label.apply(user_id: ID, tx_id: ID, category_id: ID): (label: Label)  
**where:** Transaction.owner(tx_id): ID = user_id  
**then** Transaction.mark_labeled(tx_id: ID)

---

**sync:** applyOrChangeLabelUpdatesMetrics  
**when** Label.apply(user_id: ID, tx_id: ID, category_id: ID): (label)  
**or**   Label.update(user_id: ID, tx_id: ID, new_category_id: ID): (label)  
**where** p = Transaction(tx_id).date’s period  
**then** FeedbackMetric.recompute_for_period(owner_id: ID = user_id, category_id: ID = label.category_id, period: Period = p)


---

**sync** removeLabelMovesToTrash  
**when** Label.remove(user_id: ID, tx_id: ID): (ok: Boolean)  
**where** trash_category_id = the user_id’s special Trash category ID  
**then** Label.update(user_id: ID, tx_id: ID, new_category_id: ID = trash_category_id)

---

### Brief Note on Role of Concepts  

The concepts of FlashFinance work together to support secure, user-centered expense labeling:  

- **User** establishes identity and access control so that all data (transactions, categories, labels, and metrics) remains isolated to one account.  
- **Transaction** represents immutable records parsed from uploaded bank statements; transactions cannot be manually created or edited, and the system tracks the last imported row to prevent duplicates.  
- **Category** allows flexible grouping, but categories cannot be deleted if they still contain labeled transactions. Each user also has a permanent *Trash* category: removing a label reassigns the transaction here, ensuring that once imported, every transaction is always in some category.  
- **Label** captures the explicit assignment of a transaction to a category, forming the bridge between raw records and user-defined meaning.  
- **FeedbackMetric** summarizes labeled spending over time; it is derived from transactions and labels, never edited directly, and updates automatically when labels change.  

**Design decisions:**  
- Labeling sessions must be completed for metrics to update; partial progress is not saved.  
- Transactions continue parsing from where the last import ended, avoiding redundant work.  
- Only a few common bank formats are supported at first to simplify parsing.  


## UI Sketches
![picture UI](/assets/UI_sketches.jpg)


## User Journey

Alex, a graduate student frustrated by confusing bank statements and ineffective budgeting tools, turns to FlashFinance to get clarity on his monthly spending.

After signing up and creating an account, Alex sets up a few personal categories such as Groceries, Coffee Shops, and Takeout. He uploads his latest bank statement through the secure uploader, and the app immediately generates an interactive labeling session. Transactions appear one at a time in a clean quick-pick interface, and Alex simply taps to assign each purchase to a category. Once the session is done, he notices that he accidentally labeled a coffee shop expense as groceries, he quickly corrects it with the relabel option.

Now, FlashFinance shows a simple spending summary. The totals make it clear that "Takeout" is consuming far more of his budget than he expected, while "Groceries" are steady and reasonable. 

By the end of the session, Alex feels more in control. He can see exactly where his money went, and the process felt quick rather than tedious. Instead of abandoning tracking after a week, Alex decides to upload his statements regularly, since the workflow makes reflection on spending habits both manageable and engaging.
