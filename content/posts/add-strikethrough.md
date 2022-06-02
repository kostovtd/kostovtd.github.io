---
author: "Todor Kostov"
title: "Android tricks - How to add strikethrough text in TextView"
date: "2017-01-25"
tags: [
    "android"
]
---

The strikethrough effect can be really useful in many situations. You can use it when you want to show a discount price, when you want to mark a wrong word or in many other situations. We all know that feature from software products like Word, Evernote, Sublime, etc. But how can we do the same thing with our simple [TextView](https://developer.android.com/reference/android/widget/TextView.html)?

There are two different ways to do that, based on the desired result.

If you want to have a beautiful line going through the whole length of your text, then use the code down below:

```
TextView myTextView = (TextView) findViewById(R.id.my_text_view);
myTextView.setText("Test test test");
myTextView.setPaintFlags(myTextView.getPaintFlags() | Paint.STRIKE_THRU_TEXT_FLAG);
```

Obviously, the key part is in the **setPaintFlags()** method. This method modifies something called [TextPaint](https://developer.android.com/reference/android/text/TextPaint.html). This object is an extension of the [Paint](https://developer.android.com/reference/android/graphics/Paint.html) class. It actually adds more functionality to it and it holds information about how to draw text, geometries, etc.

The other way to achieve the strikethrough effect is simpler than the one above. We can use the string resource file to define the desired text and add some HTML tags to it. Like the one down below:

```
<string name="your_string_name">Hello <strike>World</strike>!!!!</string>;
```

This is easier and more precise. Although, it has one major disadvantage, that it works only with predefined strings. If you wish to add that effect to a text taken from a network request, you must use the first approach.

## Resources

* http://stackoverflow.com/questions/3881553/is-there-an-easy-way-to-strike-through-text-in-an-app-widget

Feel free to share, comment & give your opinion on the topic!