# PowerApps Design Patterns

Disclaimer: This is based on my own experience designing and architecting a powerapps canvas app

// OnStart Rules:

/** 
  Title: Save user in a global variable and use this variable althrougout the app
  Pros: 1. You can simulate other user with minimal code changes, useful when debugging permissions
        2. Scalable and used this to manage account permissions and groups
        3. Cached user metadata and reduce API calls
**/
Set(CurrentUser, {
    Profile: Office365Users.UserProfile(User().Email),
    Image: Office365Users.UserPhoto(User().Email),
    Groups: Filter(GroupsList, User().Email in GroupMembers.Email),
    Roles: Filter(RolesList, CurrentUser.Profile.Mail in Members.Email)
});
