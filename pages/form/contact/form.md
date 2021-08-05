---
title: 'Contact Form'
form:
    fields:
        name:
            type: text
            label: Name
            validate:
                required: true
                message: 'Please enter your name!'
        email:
            type: text
            label: Email
            validate:
                type: email
                required: true
                message: 'Please enter your email address!'
        subject:
            type: text
            label: Subject
            validate:
                required: true
                message: 'Please enter a subject for your message!'
        message:
            type: textarea
            label: Message
            validate:
                required: true
                min: 10
                message: 'Email message needs to be more than 10 characters long!'
    buttons:
        submit:
            type: submit
            value: 'Send Email'
    process:
        email:
            from: '{{ form.value.email }}'
            to: '{{ config.plugins.email.to }}'
            subject: '[Contact] {{ form.value.subject|raw }}'
            body: '{{ form.value.message }}<br /><br />{{ form.value.name }}<br />{{ form.value.email }}'
        message: 'Thank you from contacting us!'
        display: /form/thankyou
published: true
recaptchacontact:
    enabled: true
    recipient: stephenobrien1979@gmail.com
    subject: 'form entry'
---

---
title: Contact Form

form:
    name: contact

    fields:
        name:
          label: Name
          placeholder: Enter your name
          autocomplete: on
          type: text
          validate:
            required: true

        email:
          label: Email
          placeholder: Enter your email address
          type: email
          validate:
            required: true

        message:
          label: Message
          placeholder: Enter your message
          type: textarea
          validate:
            required: true

        g-recaptcha-response:
          label: Captcha
          type: captcha
          recaptcha_not_validated: 'Captcha not valid!'

    buttons:
        submit:
          type: submit
          value: Submit
        reset:
          type: reset
          value: Reset

    process:
        captcha: true
        save:
            fileprefix: contact-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        email:
            subject: "[Site Contact Form] {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        message: Thank you for getting in touch!
        display: thankyou
---

# Contact form

Some sample page content
