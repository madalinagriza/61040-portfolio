# Assignment 1
## Domains:
1. Music: listening, discovering new music, and tracking listening habits.
2. Personal finance: (trying to) track spending and manage budgets.
3. Fitness: CrossFit, strength training & planning workouts.
4. Reading: exploring books in English and Romanian.
5. Biking: commuting and for recreational purposes.
6. Device management: good maintanance of personal devices.
7. Food: weekly grocery runs, meal planning, healthy eating.
8. TV & Streaming : discovering and tracking TV shows, managing streaming platforms subscriptions
9. Campus Life: staying up to date with events, social and academic opportunities
10. Photography: taking and editing photos as a beginner

Winners of most promising domains: #2, #3, #9

## Domain Problems
### Personal Finance
I think financial awareness is a super useful skill! I didn't grow up learning personal finance skills, and my attempts so far to track and understand my spendings have been inconsistent and frustrating.
I want to be more informed about where I put my money, but the tools I’ve tried haven’t worked for me. I wonder if, by identifying blocks in the process and addressing them in an app I could build, I can facilitate the process. 

#### Problem #1: High Friction in Expense Tracking

Tracking spending is either too passive (automatic apps where I don’t see specific spendings and can't internalize my habits) or too high-effort (manual spreadsheets). Both make it hard to engage meaningfully with my finances. I need a way to log expenses that is low-effort but still helps me learn what’s "a lot" and "a little" in different categories.
>> Chose this because it allows for more exploration of solutions; thinking how to maximize engagement is a fun puzzle to solve and it aligns well with what an app needs in order to work.

#### Problem #2: No Custom Categories

I struggle to differentiate between essential expenses (like groceries or campus lunch) and discretionary ones (like outings, treats, online shopping). Without flexible categories that reflect my own priorities, I can’t tell what’s adjustable when I need to cut back.
>> Not chosen; I think I already saw custom categories being offered in premium packages of an app, so functionally this already exists even if not for free.

#### Problem #3: No Separation of Funds

All my money feels clumped together in one bank account. I don’t have a mental separation between funds for necessities, savings, and optional spending, so I often overspend without realizing it. 
>> Not chosen; This could be addressed outside of software (by opening multiple accounts), so it doesn’t seem like the most compelling use of a new app.

### Fitness
I’ve been consistently working out through both CrossFit classes and my own gym routines. I enjoy how CrossFit sessions are thoughtfully structured with warmups, main workouts, and recovery periods, while solo workouts give me the freedom to focus on my own goals. Fitness has become a regular part of my routine, and I’d like to sustain this consistency while also being able to see my progress over time.

#### Problem #1: No unified tracking

When I work out at the gym on my own, I use an app called Strong to track my sets. But I don’t log anything from CrossFit classes, so there’s no unified way to see how consistent I’ve been across both. Without those records, it’s harder to recognize patterns or improvements, or how many times a week I've been active.
>> Not chosen; I excluded this because automating logs for CrossFit workouts would mean I either specifically build it for my app (which doesn't make it expandable), or I need to process a broad range of inputs. If I try to integrate AI in this processing it wouldn't make it deterministic, so overall I can't speak to the successes of such an app without much doubt.

#### Problem #2: Unfamiliar exercise names

As an international student, I often find exercise names unfamiliar and hard to map to what the movement actually does. This is especially true in CrossFit, where many exercises have unique or less intuitive names. The app I use (Strong) shows generic exercises with the muscles they target, but there’s no centralized way to get the same level of explanation for the wider variety of workouts I encounter. It takes some time to google and search what muscles are affected, correct form and tips.
>> I chose this because I can draw directly on my experience with existing apps and see a clear gap. A solution providing explanations and muscle maps for complex movements would be both useful and realistically scoped.

#### Problem #3: Disconnected from goals

When I work out, I know I want to "get stronger" or "build endurance" but it’s hard to see how my daily workouts connect to those bigger goals. CrossFit classes are pre-designed and don’t always align with my personal objectives, while my solo sessions lack structure beyond what I feel like doing. Without a way to link specific exercises to long-term progress, I sometimes feel like I’m just going through the motions.
>> Not chosen, it's valuable but broad; Mapping daily workouts to long-term goals is broad and subjective, requiring personalization that would be hard to deliver in a short project.

### Campus Life:
Since I live off-campus, it takes more effort to stay connected to what’s happening around MIT. I want to be more aware of events before they happen, whether they’re work fairs, student group activities, or social gatherings. Right now, most events come through dormspam emails, but since I routed those to my Outlook junk folder, they’re hard to sort or search through. This makes it difficult to keep track of the events that matter to me and be intentional about my involvement in campus life.


#### Problem 1: Hard to Manage Dormspam Emails

Most events I hear about arrive through dormspam, but since those messages go into my junk folder, I can’t filter or organize them. Everything is lumped together, and I can’t easily search for a specific event email later. This makes it frustrating to find the opportunities I actually care about.
>> Not chosen; I excluded this since it depends on Outlook’s junk system, which seems outside the scope of what an app can fix.

#### Problem 2: Scattered Events

Campus activities are spread across multiple channels: email, posters, dormspam, random groupchats; and there's no unified calendar. I often hear about events only after they’ve happened, which makes it easy to miss out even when I would have wanted to attend.
>> Not chosen; I excluded this because it would require coordinating with many organizers, which is too ambitious for this project and maybe not a software solution.

#### Problem 3: Lack of Follow-Through

Even when I do learn about something interesting, I don’t always follow through. There’s no simple way to 'RSVP' internally or set a reminder for myself, so I forget by the time the event actually takes place.
>> I chose this because it targets a behavioral gap common among students and can be addressed with lightweight features for the user, like reminders or event bookmarking. It’s well-scoped and does not require heavy integration with existing email platforms or websites.


## Selected problems:
### Personal Finance: high-engagement spending tracker
#### Stakeholders:
1. User: The main beneficiary. Wants a low-effort but engaging way to track spending. A better tool reduces stress, builds financial literacy, and helps them see "what’s a lot" vs. "what’s normal." 
2. Banks: Indirectly affected because better tracking means fewer disputes, fewer "surprise charges," and more informed users. They might lose some interchange fees if people cut back on discretionary spending, but they gain trust and fewer service calls. Also an important player because their statements can be used to facilitate tracking spendings.
3. Merchant: Transactions become more transparent, so patterns in spending are easier to compare. Merchants with consistently higher prices may look less favorable, while those that feel "worth it" may get more loyalty
4. Roommates/Family: Secondary stakeholders, because if the user gains control of spending, shared expenses (groceries, rent, utilities) are easier to manage and conflicts decrease.

#### Evidence
Stats:
1. [2/3 of Americans aren't reviewing their spendings.](https://finance.yahoo.com/news/survey-more-two-thirds-americans-011626600.html)
A recent survey found that more than two-thirds of Americans don’t regularly review their expenses. This supports the idea that people disengage from tracking when the process feels too difficult or time-consuming.

2. [25% of budget app users actually follow their budget goals](https://www.investopedia.com/how-many-people-actually-stick-to-a-budget-the-answer-might-surprise-you-11799284)
Although many people set up a budget, only about one in four actually stick with it. This shows the gap between intention and practice, highlighting why low-friction, engaging tracking is critical.

3. [Shared sentiment about manual tracking being hard and also error-prone.](https://zcomsolutions.com/budget-tracking-manual-vs-automated/)
Manual budget tracking with spreadsheets is often described as time-consuming and prone to mistakes. This matches my problem framing: a system that requires too much manual effort discourages people from staying engaged.

4. [Budgeting can be stressful.](https://www.reddit.com/r/budget/comments/1bnrpia/how_many_budgeters_find_it_stressinducing_is/)
Users on Reddit describe budgeting (especially manual entry) as stress-inducing and draining. This emotional weight contributes to people abandoning their trackers, reinforcing the need for designs that reduce friction.

5. [Low retention rates of finance apps (5.8% by day 30 of usage).](https://sendbird.com/blog/app-retention-benchmarks-broken-down-by-industry)
Industry data shows that only 5.8% of users are still active in finance apps after a month. This demonstrates the widespread difficulty of sustaining engagement in money-tracking apps.

6. [Apps are easy to ignore and hard to maintain.](https://www.forbes.com/sites/financialfinesse/2017/10/26/5-reasons-budgeting-apps-dont-work-for-most-people/)
Forbes reports that many budgeting apps fail because they’re easy to push aside and difficult to keep up with. This ties directly to my problem of designing an app that is simple enough to stay part of a daily routine.

7. [Comparable app: YNAB](https://www.ynab.com/pricing) YNAB is often recommended because it allows detailed labeling of expenses and active engagement with money. However, its $15/month subscription price makes it inaccessible for many students, showing a gap for simpler, cheaper alternatives.
8. [Gamification is common but underused.](https://coinlaw.io/personal-finance-app-industry-statistics/) About 32% of budgeting apps include gamification elements like streaks and challenges. This shows that designers recognize engagement is a core problem, but many tools still don’t leverage these techniques fully.
9. [Gamification boosts retention.](https://blogs.vorecol.com/blog-evaluating-the-effectiveness-of-mobile-apps-for-financial-literacy-and-wellness-161457)
Research shows apps with gamified features achieve 34% higher retention rates. This suggests that making tracking more interactive and rewarding could directly solve the engagement drop-off highlighted in my problem.

10. [Counterpoint: Some prefer automation.](https://www.reddit.com/r/personalfinance/comments/1hykvfe/what_is_the_best_budget_app_that_is_not_zerobased/) Not all users want to micromanage or label every transaction; some actually prefer automated summaries. This shows that while my problem is real, there’s also a user population that values automation over engagement, which helps me consider scope and tradeoffs.

#### Features:
1. Micro-challenges for engagement
Tracking app but with added gamification elements. "Track spendings 3 days in a row" or "track all your grocery spending": As you complete them you become more of a budget expert. 
2. Interactive Bank Statement Labeling:
Users upload their bank statement, and the app generates an interactive list of transactions. They can quickly swipe or tap to label each expense into categories, making it faster than spreadsheets while keeping you engaged with your actual spending.
3. Relative Spending Feedback:
After each expense is labeled, the app shows how that spending compares to your past habits (e.g., "20% above your usual lunch cost"). This builds intuition for what counts as "a lot" or "a little" in each category.

---
### Fitness, Unfamiliar exercise names
#### Stakeholders
- Beginner user: May have recently started working out or cannot remember exercise names. Wastes time looking up movements, risks bad form or injury, and may feel intimidated, reducing motivation to keep working out.
- Experienced user: May not need explanations for basics but could value references for less common lifts or accessory movements; a well-designed tool could broaden its appeal.
- Coach/Instructor: Spends class time re-explaining names and form; would benefit if learners came prepared or could quickly reference exercises on their own.

#### Evidence
1. [Comparable: Strong app.](https://www.strong.app/) It shows exercise names and muscle maps, how to do the exercise. Although it allows to add custom exercises, you can only add the name of the exercise and record your reps on it, no mapping to how the exercise looks
2. [CrossFit articles exist because of confusion.](https://www.wodhopper.com/crossfitlingo) Websites like Wodhopper provide long glossaries and articles explaining CrossFit terminology. The popularity of these resources highlights that many people struggle to understand the vocabulary of workouts.
3. [Exercise names aren't descriptive of the movement.](https://www.nifs.org/blog/where-do-they-come-up-with-these-exercise-names) Many common exercise names (like "good mornings" or "Turkish get-ups") give no clue about what the movement actually looks like or which muscles are involved. This makes it especially difficult for beginners or international students to understand instructions, reinforcing the need for a tool that translates jargon into clear, descriptive explanations.
4. [Fitness terminology guides are common.](https://sweat.com/blogs/fitness/fitness-terminology) Beginner resources like Sweat’s "fitness terminology" guide exist to help people learn basic terms such as HIIT, AMRAP, and 1RM. The sheer volume of onboarding information shows how intimidating exercise language can be for newcomers.
5. [Gym intimidation is widespread.](https://flexfitnessapp.com/blog/gymtimidation-survey/)
Surveys suggest that over 40% of people avoid gyms because they feel intimidated. Not knowing what exercises mean or how to do them is a major factor in this anxiety, underscoring the need for clearer explanations.

6. [Beginners quit when they don’t have clarity.](https://www.personaltraineroxford.com/-Why-Do-So-Many-People-Stop-Going-to-the-Gym-After-New-Year#:~:text=Without%20a%20clear%20plan%2C%20the,quickly%20gives%20way%20to%20frustration.&text=Walking%20into%20a%20gym%20without,a%20step%20toward%20your%20goals)
One reason new gym users stop going is that they feel intimidated and don’t have a clear plan. Confusing exercise names and unclear routines contribute to this drop-off.
7. [Lack of novelty leads to boredom.](https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2020.577522/full) Psychology research shows that repeating the same workouts causes people to lose interest and stop exercising. Exploring new movements can add novelty, but this is harder when exercise names aren’t clear.

8. [Comparable: Fitbod app.](https://app.fitbod.me/)
Fitbod has a very large database of exercises with muscle maps and video demonstrations. However, its subscription requirement creates a cost barrier, and not all users can access these explanations.

9. [Inconsistent naming frustrates even experts.](https://www.researchgate.net/publication/235728991_Towards_Standardization_of_the_Nomenclature_of_Resistance_Training_Exercises)
Researchers note that exercises often have multiple names (e.g., overhead press vs. military press), and propose standardizing terminology. This inconsistency makes it harder for beginners to find accurate guidance.

10. [Users complain when apps lack exercises](https://www.reddit.com/r/PlanetFitnessMembers/comments/1hpoow0/why_isnt_all_the_equipment_listed_in_the_app_to/)
On forums, gym members express frustration when apps don’t list the equipment or exercises they need to track. This shows that incomplete or inconsistent databases directly affect user satisfaction.

#### Features
1. Tap-for-Info Extension for CrossFit Workouts:
A browser/mobile extension designed to work with the official CrossFit website. If you highlight an exercise name in the Workout of the Day, the extension automatically searches trusted sources (like CrossFit.com’s movement library or WodHopper) and shows a quick pop-up with explanations, demo videos, or muscle groups.
Solves the problem of interrupting workouts to Google unclear names by providing instant, reliable references without leaving the page.

2. Wikipedia-Style Custom Exercise Hub:
Users can add new exercises with short descriptions, videos, or diagrams that others can view.
Addresses the fact that custom exercises in apps like Strong are just names, creating a shared, community-driven library. It can also be highly customizable, doesn't depend on a static proposed database of exercises.

3. Synonym Translator & Multi-Language Support:
Maps "Military Press" = "Shoulder Press" = "Overhead Press," and adds translations for common terms.
Perfect for international users, solving the naming inconsistency problem highlighted in research and personal experience.

---
### Campus Life, Lack of Follow-Through
#### Stakeholders
- Event organizer: Interested for people to attend their events, may deal with uncertain turnout and wasted effort when students forget events despite initial interest.
- Attendee: has to keep track of events they're interested to attend. If not attending, they miss opportunities for social and academic engagement, leading to frustration and weaker campus connection.
- Attendee's friend(s): Lose(s) out on shared experiences if plans fall through because someone forgets to follow through.

#### Evidence: 
1. [Student-campus engagement would be increased through awareness of activities (28%) and time management (26%).](https://www.insidehighered.com/news/student-success/college-experience/2024/10/01/survey-college-student-involvement-rates) A direct effect of a tool helping track events.


2. [Colleges see a decrease in club activity after the pandemic, and how the new role of clubs is to give a friend group on campus.](https://www.thelamron.com/opinion/are-college-students-losing-interest-in-clubs) This is a really important reason why increasing exposure to clubs could be crucial to helping end the loneliness epidemic among college-aged students.

3. [Comment on the necessity of new technologies to continue adapting to student needs.](https://moderncampus.com/blog/unpacking-the-problem-of-student-engagement-on-college-campuses.html) Colleges are increasingly turning to digital tools to keep up with how students find and commit to opportunities. The article suggests that student engagement software could create "virtual roadmaps" of involvement, which shows that technology-driven solutions are now expected, not optional, for boosting participation and follow-through.

4. [Student engagement at stake.](https://www.tcnjsignalnews.com/article/2024/03/opinion-joining-student-organizations-can-make-or-break-your-college-experience) Involvement can make or break your college experience, which is all the more reason why you would need an application that can make this process easier. 

5. [Survey: why students don’t join clubs.](https://www.researchgate.net/figure/Reasons-why-students-chose-not-to-join-a-club-or-society-Base-108-respondents-with_fig1_338046643)
A peer-reviewed survey found that the top reasons students didn’t join clubs included not knowing about them or not having reminders. This reinforces that awareness and follow-through are key barriers an app could solve.

6. [Fear of not fitting in.](https://thecatamount.org/3192/opinion/why-arent-students-joining-clubs/)
Some students skip clubs because they’re afraid they won’t make friends or won’t be welcomed. A tool that helps coordinate attendance with friends or show shared interest could reduce this fear.

7. [Student testimonies about declining clubs](https://thecandor.wordpress.com/2019/03/13/are-school-clubs-dying-a-discussion/) 
Articles include direct testimonies from students saying they feel clubs are "dying out" and that events aren’t reaching them beyond their first year.  It's important to keep publicizing club events to older students; better publicity and personal reminders could sustain engagement across all years.

8. [Career and leadership benefits of clubs](https://shetechsavant.medium.com/tech-community-triumphs-why-joining-college-clubs-can-transform-your-career-212d7ad17c6e)
Joining and sticking with clubs can transform a student’s career, especially by taking leadership roles as they stay involved longer. This longevity only happens if students consistently show up, which a reminder-based solution could foster.

9. [Counterpoint: some students wouldn't want increased club events engagement](https://www.uncmirror.com/article/2023/12/opinion-joining-student-organizations-can-be-a-lot-of-work-with-little-reward)
Not all students want to join clubs; some describe them as "a lot of work with little reward." This shows that while a tool could boost attendance, it must also respect that not every student will choose heavy involvement.


10. [Comparable: C!ub app.](https://launchpad.syr.edu/cub-app-connects-students-with-clubs-for-more-effective-communication/#:~:text=C!,Enterprises%20at%20the%20Martin%20J)
At Syracuse, developers created a "Cub" app to connect students with clubs and improve communication. This demonstrates demand for such tools, though it also means my design would need to differentiate and prove value.


#### Features 
1. One-Tap RSVP + Auto Reminder:
This feature allows students to mark "Interested" in an event with a single click, which automatically generates a calendar reminder shortly before the event begins. It is original because most schools rely on mass dormspam or generic calendar invites, while this design reduces friction by merging RSVP and reminder into one seamless action.

2. Personal Event Bookmark Feed:
This feature compiles all events a student has marked as "Interested" into a clean, personal feed that is separate from the clutter of dormspam or crowded inboxes. As existing event communication is scattered across posters, emails, and chats, this creates a personal "event shelf" similar to a Netflix watchlist but for campus life.

3. Friend RSVP Sync:
This feature lets students see which friends are attending an event or invite friends directly when they RSVP. Campus event tools rarely integrate social accountability, even though peer influence is a major factor in event attendance. With this, we address the reluctance to attend events alone.