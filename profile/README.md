# FollowMe
The FollowMe dApp is built for content creators, businesses, projects, and individuals who want to grow their presence within the Universal Profile and Universal Everything ecosystem. It enables follow-to-earn campaigns where new followers are rewarded with LYX or another token of your choice.

**User Flow:**
1. A user clones the FollowMe dApp to their own Universal Profile.
2. They configure the campaign: set the total reward amount and how much each follower will receive.
3. Visitors to the profile see the active campaign and can follow via the mini-app or the Universal Everything follow button.
4. New followers automatically receive a reward — but only once per profile (no abuse through follow/unfollow loops).
5. The campaign automatically ends when the total allocated tokens have been distributed.


**Architectural Diagram**

+------------------------------------+
|    Init       |
|------------------------------------|
| - LSP7: Fetch Owned Assets         |
| - LSP5: Received Assets            |
| - LSP4: Fetch Asset Metadata       |
| - LSP3: Profile Metadata           |
|   - LSP6: Key Manager (Permissions)|
|   - LSP1: UniversalReceiverDelegate|
+------------------------------------+
                |
                v
+------------------------------------+
|    Campaign Configuration          |
|------------------------------------|
| - Start Campaign                   |
|   - Set Reward & Max Spend         |
+------------------------------------+
                |
                v
+------------------------------------+
|    Permission Check & Approval     |
|------------------------------------|
| - Check FollowMe Controller Perms  |
| - Prompt User Wallet Approval (if  |
|   permissions insufficient)        |
+------------------------------------+
                |
                v
+------------------------------------+
|    FollowMe Smart Contract         |
|------------------------------------|
| - Call startCampaign()             |
|   - Register New Followers         |
|   - Set LSP1 UniversalReceiver     |
|   - Listen for LSP26 Follow Events |
+------------------------------------+


+------------------------------------+
|    Viewer Interaction (Grid)       |
|------------------------------------|
| - Fetch Active Campaign            |
| - Check:                           |
|   - Follow Status                  |
|   - Account Permissions            |
|   - UniversalReceiverDelegate      |
| - Display Campaign (if valid)      |
+------------------------------------+
                |
                v
+------------------------------------+
|    Follow Event & Reward           |
|------------------------------------|
| - Viewer Follows User              |
| - LSP26: Trigger Follow Event      |
| - FollowMe Controller Validates    |
| - Transfer Reward to Follower      |
| - Store Follower (Avoid Duplicates)|
+------------------------------------+
