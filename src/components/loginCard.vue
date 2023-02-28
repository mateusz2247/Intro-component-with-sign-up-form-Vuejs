<template>
	<div class="info">
		<h1 class="infoHeader">Learn to code by watching others</h1>
		<p class="infoParagraph">
			See how experienced developers solve problems in real-time. Watching
			scripted tutorials is great, but understanding how developers think is
			invaluable.
		</p>
	</div>

	<div class="formAndButtons">
		<p class="costBanner">
			<span class="boldedInfo"> Try it free 7 days</span> then $20/mo.
			thereafter
		</p>

		<div class="wrapper">
			<form>
				<input
					@keydown.space.prevent
					:class="{ error: !firstName && empty == true }"
					type="text"
					placeholder="First name"
					name="firstName"
					id="firstname"
					required
					v-model="firstName" />
				<p :class="{ warning: !firstName && empty == true }">
					First name cannot be empty
				</p>
				<input
					@keydown.space.prevent
					:class="{ error: !lastName && empty == true }"
					type="text"
					placeholder="Last name"
					name="lastName"
					id="lastname"
					required
					v-model="lastName" />
				<p :class="{ warning: !lastName && empty == true }">
					Last name name cannot be empty
				</p>
				<input
					@keydown.space.prevent
					:class="{ error: (!email && empty == true) || okEmail == false }"
					type="email"
					placeholder="Email"
					name="email"
					id="email"
					required
					v-model="email" />
				<p :class="{ warning: (!email && empty == true) || okEmail == false }">
					Email cannot be empty/wrong format
				</p>
				<input
					@keydown.space.prevent
					:class="{
						error: (!password && empty == true) || okPassword == false,
					}"
					type="password"
					placeholder="Password"
					name="password"
					id="password"
					required
					v-model="password" />
				<p
					:class="{
						warning: (!password && empty == true) || okPassword == false,
					}">
					Password cannot be empty(min. 8 characters)
				</p>
			</form>

			<button class="register" @click="sendData">Claim your free trial</button>

			<p class="terms">
				By clicking the button, you are agreeing to our
				<a href="#"> Terms and Services</a>
			</p>
		</div>
	</div>
</template>

<script>
import { ref } from "vue";
export default {
	name: "loginCard",
	setup() {
		let firstName = ref();
		let lastName = ref();
		let email = ref();
		let password = ref();
		let empty = ref(false);
		let okPassword = ref(true);
		let okEmail = ref(true);

		function sendData() {
			empty.value = false;
			emailValidation(email.value);
			if (
				firstName.value &&
				lastName.value &&
				email.value &&
				password.value &&
				password.value.length > 8 &&
				okEmail.value
			) {
				console.log(
					`Sent data to server: ${firstName.value} ${lastName.value} ${email.value} ${password.value}`
				);
				okPassword.value = true;
				clearFields();
			} else {
				empty.value = true;
				checkEmpty();
				console.log(
					`All field in form are required, send procedure is aborted`
				);
			}
		}
		function checkEmpty() {
			console.log("checking empty forms....");
			if (!firstName.value) {
				console.log("empty field firstName");
			}
			if (!lastName.value) {
				console.log("empty field secondName");
			}
			if (!email.value || okEmail.value == false) {
				console.log("empty field email/inccorect email");
			}
			if (!password.value || password.value.length < 8) {
				console.log("empty password/to short");
				okPassword.value = false;
			}
		}
		function clearFields() {
			firstName.value = "";
			lastName.value = "";
			email.value = "";
			password.value = "";
		}

		function emailValidation(email) {
			if (/^[^@]+@\w+(\.\w+)+\w$/.test(email)) {
				okEmail.value = true;
			} else {
				okEmail.value = false;
			}
		}

		return {
			sendData,
			firstName,
			lastName,
			email,
			password,
			empty,
			okPassword,
			okEmail,
		};
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
@import url(./style.css);
@import url(./mobile.css);
</style>
