# General Workflow
## Description
The following is a rough markup of what a potential workflow for our app could look like. This workflow is grossly oversimplified, but it defines a tight loop in which the user cannot "break" the flow.

```mermaid
flowchart TD
    start([Start]) --> userAuth{User Authenticated?}

    userAuth -.->|no| ctc[/Create Temporary Cart/]
    ctc --> pa

    userAuth -->|yes| pa[Perform Action]
    pa --> select[Choose to add an item to the cart]
    logout --> check{Logged In?}
    check -->|no| userAuth
    check -->|yes| performLogout[Log out of account]
    performLogout --> userAuth
    select -.-> add[/Add to Card/]
    add --> pa
    pa --> checkout[Check Out]
    checkout -.-> paygate[/Require payment and ship cart/]
    paygate --> term([End])

    pa --> login[Log In]
    login --> check2{Logged In?}
    check2 -->|yes| userAuth
    check2 -->|no| performLogin[Log into account]
    performLogin -.-> mergeCarts[/Merge temp cart with actual cart/]
    mergeCarts --> userAuth

    pa --> logout[Log Out]
    
```

## Noteworthy Points
This flowchart takes the liberty of assuming a few things, like allowing the user to shop without signing in and merging the temporary cart with the user's actual cart if the user decides to sign in later. It is also implied that our app will persist user carts such that the contents of the cart will remain across shopping sessions.

These are points that we as a team must discuss at some point before we start development.
