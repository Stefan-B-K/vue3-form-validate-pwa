<template>
   <div id="app">
      <ComponentsForm></ComponentsForm>
   </div>
</template>

<script setup>
import ComponentsForm from './views/ComponentsForm.vue'
</script>

<style>
html {
   -webkit-text-size-adjust: 100%;
   -webkit-font-smoothing: antialiased;
   -moz-osx-font-smoothing: grayscale;
}

body {
   margin: 0;
   font-family: "Open Sans", sans-serif;
   font-size: 16px;
   line-height: 1.5;
}

#app {
   box-sizing: border-box;
   max-width: 500px;
   padding: 0 20px 20px;
   margin: 0 auto;
}

hr {
   box-sizing: content-box;
   height: 0;
   overflow: visible;
}

a {
   color: #39b982;
   font-weight: 600;
   background-color: transparent;
}

img {
   border-style: none;
   width: 100%;
}

h1,
h2,
h3,
h4,
h5,
h6 {
   display: flex;
   align-items: center;
   font-family: "Montserrat", sans-serif;
}

h1 {
   font-size: 32px;
   font-weight: 700;
   margin-right: 20px;
}

h2 {
   font-size: 26px;
   font-weight: 700;
}

h3 {
   font-size: 22px;
   font-weight: 700;
}

h4 {
   font-size: 18px;
   font-weight: 700;
}

h5 {
   font-size: 16px;
   font-weight: 700;
}

h6 {
   font-size: 12px;
   font-weight: 700;
}

b,
strong {
   font-weight: bolder;
}

small {
   font-size: 80%;
}

.eyebrow {
   font-size: 20px;
}

.-text-primary {
   color: #39b982;
}

.-text-base {
   color: #000;
}

.-text-error {
   color: tomato;
}

.-text-gray {
   color: rgba(0, 0, 0, 0.5);
}

.-shadow {
   box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.2), 0 1px 5px 0 rgba(0, 0, 0, 0.13);
}

.badge {
   display: inline-flex;
   height: 26px;
   width: auto;
   padding: 0 7px;
   margin: 0 5px;
   background: transparent;
   border-radius: 13px;
   font-size: 13px;
   font-weight: 400;
   line-height: 26px;
}

.badge.-fill-gradient {
   background: linear-gradient(to right, #16c0b0, #84cf6a);
   color: #fff;
}

button,
label,
input,
optgroup,
select,
textarea {
   display: inline-flex;
   font-family: "Open sans", sans-serif;
   font-size: 100%;
   line-height: 1;
   margin: 0 20px 0 0;
}

button,
input {
   overflow: visible;
}

button,
select {
   text-transform: none;
}

button,
[type="button"],
[type="reset"],
[type="submit"] {
   -webkit-appearance: none;
}

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
   border-style: none;
   padding: 0;
}

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
   outline: 2px solid #39b982;
}

label {
   color: rgba(0, 0, 0, 0.5);
   font-weight: 700;
   margin-top: 5px;
}

input,
textarea {
   box-sizing: border-box;
   border: solid 1px rgba(0, 0, 0, 0.4);
}

textarea {
   width: 100%;
   overflow: auto;
   font-size: 20px;
}

[type="checkbox"],
[type="radio"] {
   display: inline-block;
   box-sizing: border-box;
   padding: 0;
   margin-right: 0.5rem;
}

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
   height: auto;
}

[type="search"] {
   -webkit-appearance: textfield;
   outline-offset: -2px;
}

[type="search"]::-webkit-search-decoration {
   -webkit-appearance: none;
}

[type="text"],
[type="date"],
[type="number"],
[type="search"],
[type="email"],
[type="password"] {
   height: 40px;
   width: 100%;
   padding: 0 10px;
   font-size: 20px;
}

[type="text"]:focus,
[type="number"]:focus,
[type="search"]:focus,
[type="email"]:focus,
[type="password"]:focus {
   border-color: #39b982;
}

::-webkit-file-upload-button {
   -webkit-appearance: button;
   font: inherit;
}

[hidden] {
   display: none;
}

.error {
   border: 1px solid red;
}

p {
   margin: 0;
}

select {
   width: 100%;
   height: 40px;
   padding: 0 24px 0 10px;
   vertical-align: middle;
   background: #fff url("data:image/svg+xml;charset=utf8,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 4 5'%3E%3Cpath fill='%23343a40' d='M2 0L0 2h4zm0 5L0 3h4z'/%3E%3C/svg%3E") no-repeat right 12px center;
   background-size: 8px 10px;
   border: solid 1px rgba(0, 0, 0, 0.4);
   border-radius: 0;
   -webkit-appearance: none;
   -moz-appearance: none;
   appearance: none;
}

select:focus {
   border-color: #39b982;
   outline: 0;
}

select:focus::ms-value {
   color: #000;
   background: #fff;
}

select::ms-expand {
   opacity: 0;
}

.field {
   margin-bottom: 20px;
}

.error {
   border: 1px solid red;
}

.errorMessage {
   color: red;
}

.button {
   display: inline-flex;
   align-items: center;
   justify-content: space-between;
   height: 50px;
   padding: 0 20px;
   margin: 20px 0;
   background: transparent;
   border: none;
   border-radius: 6px;
   text-align: center;
   font-weight: 600;
   white-space: nowrap;
   transition: all 0.2s linear;
}

.button:hover {
   -webkit-transform: scale(1.02);
   transform: scale(1.02);
   box-shadow: 0 7px 17px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.button:active {
   -webkit-transform: scale(1);
   transform: scale(1);
   box-shadow: none;
}

.button:focus {
   outline: 0;
}

.button:disabled {
   -webkit-transform: scale(1);
   transform: scale(1);
   box-shadow: none;
}

.button + .button {
   margin-left: 1em;
}

.button.-fill-gradient {
   background: linear-gradient(to right, #16c0b0, #84cf6a);
   color: #ffffff;
}

.button.-fill-gradient-reverse {
   background: linear-gradient(to right, #84cf6a, #16c0b0);
   color: #ffffff;
}

.button.-fill-gray {
   background: rgba(0, 0, 0, 0.5);
   color: #ffffff;
}

.button.-size-small {
   height: 32px;
}

.button.-icon-right {
   text-align: left;
   padding: 0 20px;
}

.button.-icon-right > .icon {
   margin-left: 10px;
}

.button.-icon-left {
   text-align: right;
   padding: 0 20px;
}

.button.-icon-left > .icon {
   margin-right: 10px;
}

.button.-icon-center {
   padding: 0 20px;
}

input + p.errorMessage {
   margin-top: 0;
   margin-bottom: 5px;
}

input.error,
select.error {
   margin-bottom: 0;
}
</style>
