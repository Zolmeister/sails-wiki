Below is an example of retrieving the UserID from session and comparing it to the userid that is passed to the server.  This will allow you to keep people from spoofing a user account.

```
// api/policies/userIdMatches.js
module.exports = function (req,res,next) {
    // Pick userId out of params
    var specifiedUserId = req.param('UserId');
    if (_.isObject(req.param('where'))) {
        specifiedUserId = req.param('where').UserId;
    }

    // If the specified user id matches the actual user id in the session, continue
    if (req.session.userId === specifiedUserId) next();
    else res.send('You don\'t have permission to use that userId.', 403);
};
```