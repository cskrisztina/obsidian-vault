
  

Reviewer should:(...)

- Label comment severity.
    

- Available labels
    

- **Praise**: Praises highlight something positive. Try to leave at least one of these comments per review. Do not leave false praise (which can be damaging). Do look for something to praise sincerely.
    
- **Nitpick**: Nitpicks are trivial preference-based requests. These requests do not block the acceptance and merge of the request and can be freely declined if the Author chooses to do so.
    
- **Suggestion:** Suggestions propose improvements to the current subject. It's important to be explicit and clear on _what_ is being suggested and _why_ it is an improvement. But as they are just a suggestion, they do not block the acceptance of the request. The Reviewer can also add their ideas and notes as suggestions.
    
- **Question:** Questions are appropriate if you have a potential concern but are not quite sure if it's relevant or not. Asking the author for clarification or investigation can lead to a quick resolution.
    
- **Issue:** Issues highlight specific problems with the subject under review. These problems are always blocking and need to be addressed before the Reviewer accepts the Merge Request.
    

- No-recheck: The Reviewer states that they trust the Author to fix the issue, and they are free to merge the Request after the problem was addressed..
    
- Recheck: The Reviewer states that after the issue is resolved, they would like to recheck the code, and will only accept the Merge Request after doing so.
    

- **Todo**: Needed changes based on discussions regarding questions or suggestions. They can also be checked with recheck or no-recheck. By default no rechecks are needed.
    

- Examples
    

- [praise] Beautifully written validation!
    
- [nitpick] I think some additional logging would be nice here
    
- [suggestion] I think this method is deprecated. Can we try and avoid its usage?
    
- [question] Won’t this change introduce a race condition?
    
- [issue (no-recheck)] We should use consts instead of vars as per our coding standard
    
- [issue (recheck)]: This will most likely not work as the event will not trigger when the user clicks a different button
    

(...)

- Make sure that
    

- The code is well-designed and performant.
    
- The code conforms to our coding guidelines.
    
- The code is safe and secure, for example:
    

- Exceptions are handled correctly.
    
- There are no vulnerabilities.
    
- Edge-cases are handled correctly.
    
- Validations are correct.
    
- Data is handled correctly.
    
- Parallel programming is done securely.
    

- The code is readable and maintainable.
    
- The developer isn’t implementing things they might need in the future but don’t know they need now.
    
- The developer used clear names for everything.
    
- The code does not contain unnecessary code duplication.
    
- The class hierarchy is correct.
    
- The code has sufficient logging to make debugging easier.
    

Both should:

- Establish and follow a process for found defects
    

- Reviewer should determine the severity of the issue and label it accordingly. (see labeling)
    
- The Author validates the issue and leaves a response for the Reviewer.
    
- If the issue was valid, the Author creates a fix in a new commit.
    
- If the issue was labeled as [no-recheck], no new Review is necessary, the Merge Request can be closed (if there are no other outstanding issues).
    
- If the issue was labeled as [recheck], the Author notifies the Reviewer.
    

- If the original Code Review was requested for a single commit, the Author should provide the new commit’s ID or URL to the Reviewer. Ideally, all of the fixes should be in a single new commit, to avoid having to Review multiple multiple commits.
    
- If the original Code Review was made in a Merge Request, the new comment will automatically be added to the Merge Request, so the Review can be continued in that Merge Request.