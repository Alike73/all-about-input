![topic banner](./images/input-banner.png)

# The hidden depths of the input element
___

The \<input\> element in HTML is indeed fascinating, with its ability to take on various behaviors and alter its appearance through the type attribute. While many of its counterparts behave similarly, the \<input\> element stands out as it encompasses everything from text input and checkboxes to switches and reset buttons for forms. In this article, I will not only describe the different types of \<input\> but also shed light on accompanying attributes that you might not be aware of, making this element more versatile and applicable in diverse scenarios. Let's dive in!
___

### Keyboard Control:

On mobile devices, when text input is selected, a virtual keyboard pops up. But what if you plan to input numbers or, for instance, an email address? In such cases, the inputmode attribute allows you to optimize the keyboard for the intended input type.

If you're entering an email address, set inputmode to email, and the @ symbol will appear on the main keyboard. If you're interested in numbers, set inputmode to numeric or decimal, displaying a panel with digits. This approach is useful when you need to enter a number but the number type isn't suitable, like when inputting a one-time password or a credit card number.

![numeric input](./images/img1.png)

The complete list of inputmode values is provided below, along with their corresponding symbols on the iOS keyboard. Android symbols may differ.

* none: disables the virtual keyboard display (used when implementing a custom keyboard, which is rarely necessary).

* text: default option.

* numeric: only numbers.

* decimal: numbers and a decimal point.

* tel: numbers and other characters for dialing a phone number.

* url: standard keyboard with a dot, forward slash, and .com instead of a space.

* email: standard keyboard with a small space, @ symbol, and dot.

* search: standard keyboard with a slightly reduced space, dot, and a highlighted "go" button replacing return.


The inputmode attribute is also supported in \<textarea\> and all elements with the contenteditable attribute.

Customize the keyboard for convenience, and your users will appreciate it.
___

### Inactive Input Elements:

If you need to display the \<input\> element but want to prevent users from altering its content or plan to modify it programmatically, the disabled attribute comes to your aid. However, it's crucial to note that disabled input elements are removed from the accessibility tree, making them inaccessible to users with special needs. Additionally, the content of disabled input elements is not sent with the form.

An alternative to the disabled attribute is the readonly attribute. It renders the field inactive, while its content remains accessible and will be submitted along with the rest of the form input.

![You can't change this](./images/img2.png)


Manuel's note: Not all screen readers announce such fields as "read-only." It's advisable to verify this first and consider providing additional descriptions if needed.

Styling readonly elements in CSS is achieved using the :read-only pseudo-class, and for elements that can be both read and written, the :read-write pseudo-class is used.

The readonly attribute is applicable only to \<input\> acting as text controls and \<textarea\> elements.

The appropriateness of using readonly instead of disabled depends on whether the element should be utilized on the page. Keep this in mind.
___

### Camera:

You might think that the only way to grant users access to their mobile device's camera and enable photo-video capturing involves using JS and the getUserMedia API. However, camera access can also be implemented declaratively. In the file upload \<input\> field, you can specify the capture attribute, which prompts the element to activate the device's camera.

Unfortunately, this feature is only available in mobile browser versions. On desktop devices, such a field will function as a standard file upload field.

On devices equipped with front and rear cameras, you can even provide instructions for using one or the other. For instance, if you ask the user to take a selfie, set capture="user" to choose the front camera. If the goal is to capture the surrounding environment, set capture="environment" to activate the rear camera. The device may override this behavior, for example, if the front camera is unavailable.

There's also the accept attribute, allowing you to specify the type of content you want to obtain from the camera. If you choose photos, the camera will activate photo-capturing mode. If you decide to record a video, it will activate video recording mode.

For example, the HTML code and its corresponding outcome are shown below:

![accept files](./images/img3.png)

This is an excellent way to take a user's photo for an avatar without using JS.
___

### Spellcheck:

Spellcheck is a versatile attribute that can be applied to any element. It activates browser

spellchecking for elements with the contenteditable="true" attribute, including elements such as \<input\>, and it definitely deserves your attention.

Different browsers handle \<input\> differently. Firefox and Safari on desktop systems won't perform spellchecking in these elements without the spellcheck attribute. On the other hand, Chrome and Safari on iOS will. To achieve consistent behavior across browsers, you should set the spellcheck attribute to true or false depending on the content of \<input\>.

For regular text, providing users with input assistance by setting spellcheck="true" is advisable. However, if the field is used for identifiers like usernames, email addresses, URLs, or other information not likely to be in the dictionary, it's better to set spellcheck="false".

It's worth noting that the actual implementation of spellchecking remains at the discretion of the browser. For instance, Chrome and Edge send the content of \<input\> elements for checking to specific services, potentially exposing the content. If your \<input\> element contains sensitive information like names, birthdates, or passwords, it's prudent to set spellcheck="false" to avoid potential risks.
___

### Automatic Shift:

On mobile devices, when entering text in an \<input\> element, the first word will default to starting with a capital letter, followed by lowercase letters. While convenient for sentence writing, situations like names and addresses require each word to begin with a capital letter. On the other hand, certain input types like flight ticket identifiers and UK postal codes demand the use of uppercase letters exclusively.

In such cases, the autocapitalize attribute comes to your aid, freeing users from the need to use Shift to input text in the desired format.

To capitalize each word, set autocapitalize="words," and for the use of exclusively uppercase letters, set autocapitalize="characters."

![autocapitalize words](./images/img4.png)

Note, that the autocapitalize attribute doesn't work where it is nonsensical, such as for \<input\> elements with types email, URL, and, most importantly, password.

Proper use of this functionality significantly eases data input for your users on mobile devices.
___

### Less Input, Better Experience:

To conclude this crash course, I decided to highlight my favorite attribute for input fields – autocomplete.

It guides the browser in suggesting input completion options based on known expressions. The autocomplete attribute can take a vast array of values, associating \<input\> with various things the browser knows or can learn.

For actions like registration or login, you can set autocomplete to values like username or email. For passwords, you can use the value new-password to prevent the browser from autofilling an existing password and prompt the user to enter a new one. Additionally, the value current-password can be used to allow the browser or password manager to automatically fill in a known password.

For address autofill, use values like street-address, country-name, and postal-code. In commercial forms, you can enhance these values with specifying identifiers to differentiate between billing and shipping addresses.

![autocomplete name](./images/img5.png)

For one-time passwords sent via SMS, you can use the value one-time-password, instructing the browser to view recent messages and extract the one-time password for autofill.

In the case of implementing access keys, you can use the value webauthn for autocomplete to involve autofill in the process.

When used intelligently, autocomplete alone can meet the WCAG AA level "Input Purpose" rule. By providing detailed instructions to the browser about the expected content type of input fields, we not only save users time but also spare them unnecessary typing.

However, there are instances where you need to disable autocomplete entirely. Setting autocomplete="off" disables the browser from remembering entered text. This solution is relevant for fields where different input is expected each time, such as CAPTCHA.

Using the right autocomplete attributes significantly streamlines the text input process for users.
___

### Choosing the Right Attributes:

Designing and developing forms that cater to all users can be challenging. However, the \<input\> element provides numerous options to make text forms more user-friendly and accessible.

For managing virtual input keyboards, utilize inputmode. If you want to disable the ability to edit \<input\> while retaining the ability to read and submit it, opt for readonly instead of disabled. Activating the camera on mobile devices can be achieved with the capture attribute. The spellcheck attribute enables spellchecking, but it's crucial to remember to disable it for sensitive input. Additionally, you can save users time with autocapitalize by regulating capitalization rule.