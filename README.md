# vue-password

> A Vue.js password input component that includes a toggle to show the password and a strength meter using the [Dropbox zxcvbn](https://github.com/dropbox/zxcvbn) library.

## Screenshot

![Screenshot](https://raw.githubusercontent.com/skegel13/vue-password/v0.0.6/vue-password.png)

## Install

Install the package using npm.

    $ npm install vue-password

Register the component.

    import Vue from 'vue'
    import VuePassword from 'vue-password'

    Vue.component(VuePassword)

## Usage

Use the prop in your HTML and apply a v-model attribute for the password and any additional props for the desired configuration. The following example shows how vue-password could be used in a registration form using the [Bulma CSS Framework](http://bulma.io/).

### Javascript

    import Vue from 'vue'
    import VuePassword from 'vue-password'

    new Vue({
      el: '#app',
      components {
        VuePassword
      },
      data {
        user: {
          email: '',
          password: ''
        }
      }
    })

### HTML

    <form>
      <label for="email">Email</label>
      <p class="control">
          <input id="email" class="input" type="email" name="email" v-model="user.email">
      </p>

      <label for="password">Password</label>
      <p class="control">
          <vue-password v-model="user.password"
                        classes="input"
                        :user-inputs="[user.email]"
          >
          </vue-password>
      </p>

      <p class="control">
          <button class="button is-primary">Register</button>
      </p>
    </form>

![Screenshot](https://raw.githubusercontent.com/skegel13/vue-password/v0.0.6/vue-password-bulma-example.png)

## Props

Use the following props to configure the password input.

| Prop | Default | Description |
| ---- | :-----: | ----------- |
| id | 'password' | Set the ID of the input element. |
| name | 'password' | Set the name attribute of the input element. |
| classes | 'form-control' | Set the classes for the input element. The default is the 'form-control' class used by Twitter Bootstrap. A string or array of classes can be passed in the prop. |
| minlength | 8 | Set the minlength HTML5 validation attribute for the input element. |
| maxlength | 200 | Set the maxlength HTML5 validation attribute for the input element. |
| required | true | Set the required HTML5 validation attribute for the input element. |
| pattern | '' Set the pattern HTML5 validation attribute for the input element. |
| strengthClasses | ['PasswordInput--very-weak', 'PasswordInput--weak', 'PasswordInput--medium', 'PasswordInput--good', 'PasswordInput--great'] | Set the classes used to style the strength message and strength meter. This should be an array of five classes. The classes are applied depending on the current strength score of the password (0-4). |
| strengthMessages | ['Very Weak', 'Weak', 'Medium', 'Strong' 'Very Strong'] | Set the messages that appear depending on the strength score of the password. This should be an array of five messages. |
| userInputs | [] |  Set any additional strings for improving the strength calculation. For example, add values for username or email fields so if the password contains those items, it will receive a lower strength. [Click here](https://github.com/dropbox/zxcvbn#usage) for more information. |
| disableToggle | false | Disable the password input toggle to show/hide the password. |
| disableStrength | false | Disable the password strength meter and messages. |

## Slots

[Named slots](https://vuejs.org/v2/guide/components.html#Named-Slots) can be used to change the layout of the password toggle, strength meter, and strength messages.

| Slot | Scope | Description |
| ---- | ----- | ----------- |
| password-toggle | toggle method to change the input type attribute from 'password' to 'type' | Use this named slot to change the layout of the password toggle. |
| strength-meter | stength object provided by [zxcvbn](https://github.com/dropbox/zxcvbn#usage) | Use this named slot to change the layout of the password strength meter. |
| strength-message | stength object provided by [zxcvbn](https://github.com/dropbox/zxcvbn#usage) | Use this named slot to change the layout of the password strength messages. |

### Example: Change password toggle to text button

    <vue-password v-model="user.password">
        <template slot="password-toggle" scope="props">
            <button class="VuePassword__Toggle"
                    type="button"
                    v-on:click = "props.toggle"
                    v-text="props.type === 'password' ? 'SHOW' : 'HIDE'"
            >
            </button>
        </template>
    </vue-password>

![Screenshot](https://raw.githubusercontent.com/skegel13/vue-password/v0.0.6/vue-password-slots.png)
