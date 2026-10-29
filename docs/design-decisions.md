Gaps worth noting

1. “Unassessed” is not defined.
The document says unassessed risks are excluded from the heat map, but never says what makes a risk unassessed. The simplest rule: a risk with status Identified is unassessed; Assessed or any later status is assessed. That ties the heat map directly to the status field, so no extra column is needed.

2. Actions assigned across owners.
A Risk Owner can create an action on their own risk. If they assign it to another Risk Owner, that person can update it (“assigned directly to them”) but isn’t allowed to see risks they don’t own. Decide what the assignee sees. I’d suggest: any active user can be an action owner, and the assignee sees the action plus the linked risk’s title only, nothing else.

3. Control pages could leak other owners’ risks.
Risk Owners can view all controls, but a control page might list every risk linked to it. For a Risk Owner, filter that list to their own risks. This matches your rule that they never see information about other owners’ risks, and it’s a good test case.

4. Unlinking controls.
Risk Owners can link controls to their own risks, but unlinking isn’t mentioned. Allow it for own risks, and audit both link and unlink events (the audit list doesn’t currently include them).

5. Deactivating a user who owns things.
If an Admin deactivates a Risk Owner, their risks and actions would be stuck. Simple rule: deactivation is blocked until the user’s open risks and actions are reassigned.

6. Small table cleanup.
In the access summary, the row “View own risks and related dashboard information” shows Yes for Admin. It’s harmless, but the Admin already sees everything, so the row only matters for Risk Owners.

7. Optional: concurrency on other records.
RowVersion is only on Risks. Controls and actions can also be edited by two people at once. Adding the same token to them is cheap. Leave it for later if you’re short on time.