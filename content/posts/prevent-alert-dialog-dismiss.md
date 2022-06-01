---
author: "Todor Kostov"
title: "Android tricks - How to prevent AlertDialog from dismissing after onClick event?"
date: "2019-12-08"
tags: [
    "android"
]
---

Have you noticed that the default behavior of [AlertDialog](https://developer.android.com/reference/android/app/AlertDialog.html) is to disappear after onClick event? I'm sure you have! But there are cases when we actually don't want to dismiss the dialog. In these situation, the default behavior of the AlertDialog must be overridden. Down below you will find a snippet which is doing exactly that thing.

{{< gist kostovtd dbbacf70012793c317ac4c3b3c1f445c >}}

## Code description

So what exactly is happening in that snippet? You can see that when we are constructing the AlertDialog object by using the Builder Pattern, we are setting null parameters to the methods responsible for setting up the behavior of the positive and the negative buttons.

```
.setPositiveButton(android.R.string.ok, null)
.setNegativeButton(android.R.string.cancel, null)
```

The null parameters are actually the onClickListeners for these buttons. We are doing this, because later on we will override the behavior of these buttons. Of course, you can try to provide click listeners there, but no matter what you will include in these listeners, your AlertDialog will disappear after the event. If you want to dive deeper into the reasons for that, I highly recommend you to go through the StackOverflow discussion listed in the 'References' part!

The place where we are overriding the behavior of the positive and the negative buttons is in the onShow() method included in OnShowListener.

```
dialog.setOnShowListener(new DialogInterface.OnShowListener() {
    @Override
    public void onShow(DialogInterface dialog) {
        Button button = ((AlertDialog) dialog).getButton(AlertDialog.BUTTON_POSITIVE);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                // TODO Do something
            }
        });
    }
});
```

But why there? It's simple! Because, this listener will be invoked when the dialog is shown. Sooo what?! Well... if this listener is invoked when the dialog is shown that means that whatever was set, behind the scenes, to these particular buttons, can be overridden by us. So, in this particular case it is not enough just to ask 'how' to override this behavior, but you have to ask 'when' as well.

**Please, notice that this approach will work only for Android API > 8.**

## Resources

* http://stackoverflow.com/questions/2620444/how-to-prevent-a-dialog-from-closing-when-a-button-is-clicked

Feel free to share, comment & give your opinion on the topic!
