# Airship CMS Forms
Download the repository files at [https://github.com/AirshipCMS/contact-forms.airshipcms.io](https://github.com/AirshipCMS/contact-forms.airshipcms.io). See an example of the live form at [https://contact-forms.airshipcms.io](https://contact-forms.airshipcms.io).

---

## Step 1. Set up the Collection
In Airship CMS Admin, set up a new collection.

### Collection Setup
Pay attention to the **Public Path**. This is important for creating the email template for this form.

![collection-setup](https://user-images.githubusercontent.com/1865400/29060441-806f6dd8-7bb5-11e7-99cf-f7ad80740e4d.png)

### Collection Rendering
Skip this. You don't need to set a layout or template directory.

### Collection Settings
![collection-settings](https://user-images.githubusercontent.com/1865400/29060440-8060e506-7bb5-11e7-906d-aa2abbcccf5d.png)

### Post Fields
Create fields that correlate to the data you want to save in your form. **It is easiest to save all data as Text**, though if you want to manipulate data after submission, you can also save data as radio, select, and checkbox field types. This example collection shows many different field types, though if you are making a simple contact form, you only need to set the field types you need:

![post-fields](https://user-images.githubusercontent.com/1865400/29060442-806f825a-7bb5-11e7-9397-a5d28f5cba0c.png)

### Primary Label
Leave it as Created At.

![primary-label](https://user-images.githubusercontent.com/1865400/29060439-805c424e-7bb5-11e7-94df-29c382b55dd1.png)

### Untested Field Types
Field types that have not been tested with forms: Multiselect, Richtext Area, Image, Link, List of Images, List of Links, Related Aerostats, Date.

---

## Step 2. Set a BCC Public Make Email
In Airship CMS Admin, go to **Settings** and add an email to BCC Public Make in order to receive emails when someone enters a form submission.

![bcc-publicmakesetting](https://user-images.githubusercontent.com/1865400/29060444-8078786a-7bb5-11e7-86ce-3d953ef88e52.png)

---

## Step 3. Create a Page for the form to render on.
In Airship CMS Admin, create a Page called "Contact" with permalink "/contact" and template "contact.html".

![contact-page](https://user-images.githubusercontent.com/1865400/29060965-a47f227a-7bb7-11e7-88dc-10880e1ebf92.png)

---

## Step 4: Set up the Contact Form Page Template
In your text editor, create the `contact.html` page template, and add the form fields you need. Reference the `contact.html` template in the example repository.

Be sure to add links to the necessary scripts to make the form work:
```
<script src="//code.jquery.com/jquery-3.2.1.min.js"></script>
<script src="/assets/scripts/contact.js"></script>
```

---

## Step 5: Modify the Contact Form Javascript

### Find the Collection ID.
In Airship CMS, click the wrench icon to Modify the Collection, and find the **Collection ID**.

![collection-id](https://user-images.githubusercontent.com/1865400/29060438-805c1918-7bb5-11e7-8030-0488b826b0ee.png)

Remember the ID number. You don't need to save any changes.

### Modify the Javascript
In your text editor, modify the `contact.js` so that the form submits to the proper collection on your site. In the javascript file on `line 7` change the Collection ID to the ID for your collection.

```
url: "/api/aerostat_collections/373",
```

---

## Step 6: Test the Contact Form
With this markup & script, you can test locally that the form creates a post in the Contact Form Example collection.

If everything is set up properly, hitting the Submit button on your local form will create an example post in your collection:

![submission-example](https://user-images.githubusercontent.com/1865400/29060885-5a3a62d8-7bb7-11e7-92cf-ef0b37837be7.png)

When you view the post, it will look something like this:

![post-example](https://user-images.githubusercontent.com/1865400/29060443-807042bc-7bb5-11e7-8c9b-811b61d48186.png)

You will notice that even though the post has been created, you haven't received any email notifications.

---

## Step 7: Create Email Templates
Before setting up the email template, make sure everything else is set up properly.
- [x] You have added at least one BCC Public Make Email
- [x] Submissions are being created in your collection when you Submit them though your local form.

### `airmail.html`
This layout is required in order for email submissions to work. It is just a container layout and does not contain any markup that will be used in the actual email.

### `contact-form-example_email.html`
This template is required in order for email submissions to work. This template contains markup that will be used in the email template. **Note: the email template name is the collection public path with `_email.html` appended to the end.** In this example collection, the public path is `contact-form-example`, so the email template name needs to be `contact-form-example_email.html`.

![email-name](https://user-images.githubusercontent.com/1865400/29061827-20c8b366-7bbb-11e7-804c-3c22d4cadbe4.png)

---

## Step 8: Launch your Form Files
You must `airship launch` the email templates in order for the email notification to work. Changes to local airmail templates have no effect. Only LAUNCHED email templates will be read by the email server.

---

## Step 9: Test your Form
Test the form on your launched website. You should see a post in the collection in Airship CMS Admin, and you should also receive an email submission notifying you about the submission.

---
For security reasons and to prevent abuse, you cannot send public make submission notifications to arbitrary emails. Emails will only send to the emails listed in the BCC Public Make Email List in the Admin Panel.
