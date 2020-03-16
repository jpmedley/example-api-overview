---
recipe: api-feature
title: 'ContactsManager'
mdn_url: /en-US/docs/Web/API/ContactsManager
specifications: https://wicg.github.io/contact-api/spec/#contacts-manager
browser_compatibility: api.ContactsManager
---

## Description

The `ContactsManager` interface of the Contact Picker API provides methods for prompting users to select entries from their contact list and share limited details of the selected entries with a website. It allows users to share only what they want, when they want. 

For example, a web-based email client could use the Contact Picker API to select the recipient(s) of an email. A voice-over-IP app could look up which phone number to call. Or a social network could help a user discover which friends have already joined.

## Properties

`**ContactsManager.getProperties()**`

Returns the properties that are supported by the underlying system. The returned properties may be any of: `"name"`, `"email"`, `"tel"`, `"address"`, or `"icon"`.

`**ContactsManager.select()**`

Returns a promise and shows the contact picker, allowing the user to select the contact or contacts they want to share with the site. After selecting what to share and clicking Done, the promise resolves with an array of contacts selected by the user.

When calling select() you must provide an array of properties you\'d like returned as the first parameter with the allowed values being any of: `"name"`, `"email"`, `"tel"`, `"address"`, or `"icon"`. The second, optional parameter specifies whether multiple contacts can be selected by the user.

## Examples

The following example shows how to use `ContactsManager.select()`. After calling `select()` with the desired properties, a contact picker is shown to the user. The returned promise does not resolve until the user closes the contact picker. If the user selected contacts, the promise resolves with an array of `ContactProperties`. 

```js
const props = ['name', 'email', 'tel', 'address', 'icon'];
const opts = {multiple: true};

try {
  const contacts = await navigator.contacts.select(props, opts);
  handleResults(contacts);
} catch (error) {
  // Handle any errors here.
}
```

The `ContactProperties` array from the resolved promise.

```json
[{
  "email": [],
  "name": ["Queen O'Hearts"],
  "tel": ["+1-206-555-1000", "+1-206-555-1111"]
},
{
  "email": [],
  "name": ["Jack O'Diamonds"],
  "tel": ["+1-816-555-1970", "+1-816-555-1973"]
}]
```
