<template>
<div class="form-card">
    <form action="#" method="get" class="form signup-form" @submit.prevent="submitForm">
        <div class="form__group">
            <input class="form__input" :class="{ 'form__input__error-border': error.first_name.has_error}" type="text" name="first_name" :placeholder="placeholder.first_name" id="first_name" v-model="first_name">
            <div class="form__input__error-container" v-show="error.first_name.has_error">
                <span class="form__input__error-container--error-message">{{ error.first_name.current_message }}</span>
                <img class="form__input--error-icon" src="../assets/images/icon-error.svg" alt="error icon">
            </div>
        </div>
        <div class="form__group">
            <input class="form__input" :class="{ 'form__input__error-border': error.last_name.has_error}" type="text" name="last_name" :placeholder="placeholder.last_name" id="last_name" v-model="last_name">
            <div class="form__input__error-container" v-show="error.last_name.has_error">
                <img class="form__input--error-icon" src="../assets/images/icon-error.svg" alt="error icon">
                <span class="form__input__error-container--error-message">{{ error.last_name.current_message }}</span>
            </div>
        </div>
        <div class="form__group">
            <input class="form__input" :class="{ 'form__input__error-border': error.email.has_error, 'form__input__error-email': error.email.has_error }" type="email" name="email" :placeholder="placeholder.email" id="email" v-model="email">
            <div class="form__input__error-container" v-show="error.email.has_error">
                <img class="form__input--error-icon" src="../assets/images/icon-error.svg" alt="error icon">
                <span class="form__input__error-container--error-message">{{ error.email.current_message }}</span>
            </div>
        </div>
        <div class="form__group">
            <input class="form__input" :class="{ 'form__input__error-border': error.password.has_error}" type="password" name="password" :placeholder="placeholder.password" id="password" v-model="password">
            <div class="form__input__error-container" v-show="error.password.has_error">
                <img class="form__input--error-icon" src="../assets/images/icon-error.svg" alt="error icon">
                <span class="form__input__error-container--error-message">{{ error.password.current_message }}</span>
            </div>
        </div>
        <div class="form__group">
            <input class="btn btn--green" type="submit" value="Claim Your Free Trial">
        </div>
        <p class="form__t&s">
            By clicking the button, you are agreeing to our <a href="#" class="color-red">Terms and Services</a>
        </p>
    </form>
</div>
</template>

<script>
export default {
    data() {
        return {
            first_name: '',
            last_name: '',
            email: '',
            password: '',
            placeholder: {
                first_name: 'First Name',
                last_name: 'Last Name',
                email: 'Email Address',
                password: 'Password',
            },
            error: {
                first_name: {
                    has_error: false,
                    current_message: '',
                    messages: {empty: 'First Name cannot be empty'}
                },
                last_name: {
                    has_error: false,
                    current_message: '',
                    messages: {empty: 'Last Name cannot be empty'}
                },
                email: {
                    has_error: false,
                    current_message: '',
                    messages: {format: 'Looks like this is not an email'}
                },
                password: {
                    has_error: false,
                    current_message: '',
                    messages: {empty: 'Password cannot be empty'}
                }
            },
        }
    },
    watch: {
        first_name(sNew) {
            this.isEmpty(sNew, 'first_name');
        },
        last_name(sNew) {
            this.isEmpty(sNew, 'last_name');
        },
        password(sNew) {
            this.isEmpty(sNew, 'password');
        },
        email(sNew) {
            this.validateEmail(sNew);
        }
    },
    methods: {
        isEmailFormat(sEmail) {
            const emailFormatRegex = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
            return emailFormatRegex.test(sEmail);
        },
        submitForm() {
            this.validateFormData();
        },
        validateFormData() {
            const bFormHasError = [
                this.isEmpty(this.first_name, 'first_name'),
                this.isEmpty(this.last_name, 'last_name'),
                this.isEmpty(this.password, 'password'),
                this.validateEmail(this.email),
            ].some((bHasError) => bHasError);
            if (bFormHasError === false) {
                alert('Success!');
            }
        },
        validateEmail(sEmail) {
            const THIS = this;
            const INVALID_EMAIL_PLACEHOLDER = 'email@example/com'
            const INPUT_NAME = 'email';
            const EMAIL_VALIDATIONS = [
                {
                    message_type: 'format', is_invalid: THIS.isEmailFormat(sEmail) === false
                }
            ];
            const HAS_ERROR = this.renderValidator(INPUT_NAME, EMAIL_VALIDATIONS);
            if (HAS_ERROR) {
                this.placeholder.email = INVALID_EMAIL_PLACEHOLDER;
            }
            return HAS_ERROR;
        },
        isEmpty(sText, sInputName) {
            const INPUT_VALIDATIONS = [
                {
                    message_type: 'empty', is_invalid: sText.length === 0
                }
            ];
            return this.renderValidator(sInputName, INPUT_VALIDATIONS);
        },
        renderValidator(sInputName, aValidations) {
            this.error[sInputName].has_error = aValidations.some((oValidation) => {
                if (oValidation.is_invalid) {
                    this.showErrorMessage(sInputName, oValidation.message_type);
                }
                return oValidation.is_invalid;
            });
            return this.error[sInputName].has_error;
        },
        showErrorMessage(sInputName, sErrorType) {
            this.error[sInputName].current_message = this.error[sInputName].messages[sErrorType];
        }
    }
}
</script>