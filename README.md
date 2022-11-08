# Cookie Banner Project

This is a Vue.js cookie banner component for informing users about cookie use and, if necessary, obtaining consent for cookie use. Accepted or rejected cookie settings are saved in localStorage.

![Cookie Banner](https://user-images.githubusercontent.com/14932895/195907532-e33821fd-643f-467b-bfd9-794bf803b7e9.gif)

## [Check out the live example.](https://vue-cookie-ten.vercel.app/)

## Usage

### Props

| Prop                   | Type    | Description                                | Default                                                                             |
| ---------------------- | ------- | ------------------------------------------ | ----------------------------------------------------------------------------------- |
| settings               | Array   | Items to show in Cookie Settings Tab       | [{name:'Option-I', status:true}]                                                    |
| title                  | String  | Title to show the top of the banner        | "Title"                                                                             |
| description            | String  | Text to show in the banner for information | We baked some cookies that you have to accept, if you want to enjoy this website... |
| policyText             | String  | Text to show in the Cookie Policy Tab      | Lorem ipsum dolor sit amet consectetur adipisicing elit...                          |
| rejectButtonVisibility | Boolean | Visibility state of the Reject button      | true                                                                                |

### Event Emits

- This component just emits 'buttonClick' event and it returns clicked button's title.

### Technologies:

- [Vue.js](https://vuejs.org/)
- [TailwindCSS](https://tailwindcss.com/)
