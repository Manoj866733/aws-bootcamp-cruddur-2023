# Week 3 — Decentralized Authentication

This was the week 3 of the bootcamp. It was another changelling week with alot of new stuffs to learn. In this week I setup Amazon cognito and we changed the UI of our cruddur application.

## Setup Cognito User-pool
Using the Amazon Console, I was able to create a user-pool with the following steps.
 * In AWS console search for Amazon Cognito
 * Select create new user pool
 * In Cognito user pool sign-in options, Select only email as shown below
  
  ![image](https://user-images.githubusercontent.com/100923201/226099084-829667dc-471f-4ca5-9478-6b101f097f82.png)
 
 * In password policy select Cognito default and select no MFA in the bottom

![image](https://user-images.githubusercontent.com/100923201/226099200-d4caed08-62e1-4035-abfd-d13651b298c3.png)

 * In Configure sign-up experience page, Uncheck Self-registration and for Required attributes select the options as shown below.

![image](https://user-images.githubusercontent.com/100923201/226099336-419fa58f-de97-47e3-a6c4-ee60ccb5468a.png)

 * In Configure message delivery, Select Send email with Cognito
 * In Integrate your app page, We can set up app integration for our user pool with Cognito's built-in authentication and authorization flows. 
 * Finally, confirm the user-pool details and home page should be as shown below
 
 ![image](https://user-images.githubusercontent.com/100923201/226099447-7f93ae16-f28d-41ca-9dc6-fe6b123ae460.png)

# Install AWS Amplify library

## Setup Environment Variables for Frontend and Enabling Signing in

1. To interact with aws-cognito from the frontend, we need to install aws-amplify nodes. From the command line, I navigated to the frontend folder. Then I ran the following command:

```$ npm i aws-amplify --save```

2. Then we need to add Env Vars in the docker-compose.yml file:

```
  frontend-react-js:
    environment:
      REACT_APP_AWS_PROJECT_REGION: "${AWS_DEFAULT_REGION}"
      REACT_APP_AWS_COGNITO_REGION: "${AWS_DEFAULT_REGION}"
      REACT_APP_AWS_USER_POOLS_ID: "us-east-1_*******"
      REACT_APP_CLIENT_ID: "*********************"
```


3. Edit app.js file 

```import { Amplify } from 'aws-amplify';

Amplify.configure({
    "AWS_PROJECT_REGION": process.env.REACT_AWS_PROJECT_REGION,
    "aws_cognito_identity_pool_id": process.env.REACT_APP_AWS_COGNITO_IDENTITY_POOL_ID,
    "aws_cognito_region": process.env.REACT_APP_AWS_COGNITO_REGION,
    "aws_user_pools_id": process.env.REACT_APP_AWS_USER_POOLS_ID,
    "aws_user_pools_web_client_id": process.env.REACT_APP_CLIENT_ID,
    "oauth": {},
    Auth: {
        // We are not using an Identity Pool
        // identityPoolId: process.env.REACT_APP_IDENTITY_POOL_ID, // REQUIRED - Amazon Cognito Identity Pool ID
        region: process.env.REACT_AWS_PROJECT_REGION,           // REQUIRED - Amazon Cognito Region
        userPoolId: process.env.REACT_APP_AWS_USER_POOLS_ID,         // OPTIONAL - Amazon Cognito User Pool ID
        userPoolWebClientId: process.env.REACT_APP_AWS_USER_POOLS_WEB_CLIENT_ID,   // OPTIONAL - Amazon Cognito Web Client ID (26-char alphanumeric string)
    }
}); 
```


4. Edit homefeedpage.js

```
import { Auth } from 'aws-amplify';

// set a state
const [user, setUser] = React.useState(null);

// check if we are authenicated
const checkAuth = async () => {
  Auth.currentAuthenticatedUser({
    // Optional, By default is false. 
    // If set to true, this call will send a 
    // request to Cognito to get the latest user data
    bypassCache: false 
  })
  .then((user) => {
    console.log('user',user);
    return Auth.currentAuthenticatedUser()
  }).then((cognito_user) => {
      setUser({
        display_name: cognito_user.attributes.name,
        handle: cognito_user.attributes.preferred_username
      })
  })
  .catch((err) => console.log(err));
};

// check when the page loads if we are authenicated
React.useEffect(()=>{
  loadData();
  checkAuth();
}, [])
```

5. Edit DesktopNavigation.js
```
import './DesktopNavigation.css';
import {ReactComponent as Logo} from './svg/logo.svg';
import DesktopNavigationLink from '../components/DesktopNavigationLink';
import CrudButton from '../components/CrudButton';
import ProfileInfo from '../components/ProfileInfo';

export default function DesktopNavigation(props) {

  let button;
  let profile;
  let notificationsLink;
  let messagesLink;
  let profileLink;
  if (props.user) {
    button = <CrudButton setPopped={props.setPopped} />;
    profile = <ProfileInfo user={props.user} />;
    notificationsLink = <DesktopNavigationLink 
      url="/notifications" 
      name="Notifications" 
      handle="notifications" 
      active={props.active} />;
    messagesLink = <DesktopNavigationLink 
      url="/messages"
      name="Messages"
      handle="messages" 
      active={props.active} />
    profileLink = <DesktopNavigationLink 
      url="/@andrewbrown" 
      name="Profile"
      handle="profile"
      active={props.active} />
  }

  return (
    <nav>
      <Logo className='logo' />
      <DesktopNavigationLink url="/" 
        name="Home"
        handle="home"
        active={props.active} />
      {notificationsLink}
      {messagesLink}
      {profileLink}
      <DesktopNavigationLink url="/#" 
        name="More" 
        handle="more"
        active={props.active} />
      {button}
      {profile}
    </nav>
  );
}
```

6. Edit ProfileInfo.js

```
import { Auth } from 'aws-amplify';

const signOut = async () => {
  try {
      await Auth.signOut({ global: true });
      window.location.href = "/"
  } catch (error) {
      console.log('error signing out: ', error);
  }
}
```

7. Edit DesktopSidebar.js
```
import './DesktopSidebar.css';
import Search from '../components/Search';
import TrendingSection from '../components/TrendingsSection'
import SuggestedUsersSection from '../components/SuggestedUsersSection'
import JoinSection from '../components/JoinSection'

export default function DesktopSidebar(props) {
  const trendings = [
    {"hashtag": "100DaysOfCloud", "count": 2053 },
    {"hashtag": "CloudProject", "count": 8253 },
    {"hashtag": "AWS", "count": 9053 },
    {"hashtag": "FreeWillyReboot", "count": 7753 }
  ]

  const users = [
    {"display_name": "Andrew Brown", "handle": "andrewbrown"}
  ]

  let trending;
  let suggested;
  let join;
  if (props.user) {
    trending = <TrendingSection trendings={trendings} />
    suggested = <SuggestedUsersSection users={users} />
    } else {
      join = <JoinSection />
    }
  
  return (
    <section>
      <Search />
      {trending}
      {suggested}
      {join}
      <footer>
        <a href="#">About</a>
        <a href="#">Terms of Service</a>
        <a href="#">Privacy Policy</a>
      </footer>
    </section>
  );
}
```

# Create a user through the Console

![image](https://user-images.githubusercontent.com/100923201/226104682-90672053-8333-4259-ae74-3fefebac5122.png)

# Verify said user through the CLI

```aws cognito-idp admin-set-user-password --user-pool-id "us-east-1_******" --username ******* --password ****** --permanent```

# Sign-in Page

```import {Auth} from 'aws-amplify';

const [errors, setErrors] = React.useState('');

const onsubmit = async (event) => {
    setErrors('')
    event.preventDefault();
    try {
        Auth.signIn(username, password)
            .then(user => {
                localStorage.setItem("access_token", user.signInUserSession.accessToken.jwtToken)
                window.location.href = "/"
            })
            .catch(err => {
                console.log('Error!', err)
            });
    } catch (error) {
        if (error.code == 'UserNotConfirmedException') {
            window.location.href = "/confirm"
        }
        setErrors(error.message)
    }
    return false
}

let errors;
if (errors) {
    errors = <div className='errors'>{errors}</div>;
}

// just before submit component
{
    errors
}
```

![Screenshot 2023-03-16 154102](https://user-images.githubusercontent.com/100923201/226104752-1bbc3548-f1f3-4d88-963a-1c68c558bded.png)


![homepage](https://user-images.githubusercontent.com/100923201/226104782-502ac73f-80a2-4997-84e4-23bb43d2cdbe.png)

## Authenticated  in debug

![Screenshot 2023-03-17 234951](https://user-images.githubusercontent.com/100923201/226104799-cb595bad-bf0e-4fee-a23d-0ff805c637e0.png)

## Customised frontend homepage

![Before signout](https://user-images.githubusercontent.com/100923201/226104868-36256eb1-07a3-4cd1-8c33-ad53f691ff0d.png)


## Improving UI Contrast and Implementing

![Screenshot 2023-03-18 152020](https://user-images.githubusercontent.com/100923201/226104907-79180dde-756b-4e7a-af47-aded561ba83e.png)

