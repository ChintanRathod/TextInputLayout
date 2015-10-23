# TextInputLayout

TextInputLayout are part of DesignSupportLibrary provided by Android in version 23. 

TextInputLayout is a good widget which is replacement of EditText. In this sample application, you will find how you can use TextInputLayut. You can also find how to change hint color of it and how to apply Typeface.

# How to apply Typeface

    private void setTypefaceToInputLayout(TextInputLayout inputLayout, String typeFace){

        final Typeface tf = Typeface.createFromAsset(getAssets(), typeFace);

        inputLayout.getEditText().setTypeface(tf);
        try {
            // Retrieve the CollapsingTextHelper Field
            final Field collapsingTextHelperField = inputLayout.getClass().getDeclaredField("mCollapsingTextHelper");
            collapsingTextHelperField.setAccessible(true);

            // Retrieve an instance of CollapsingTextHelper and its TextPaint
            final Object collapsingTextHelper = collapsingTextHelperField.get(inputLayout);
            final Field tpf = collapsingTextHelper.getClass().getDeclaredField("mTextPaint");
            tpf.setAccessible(true);

            // Apply your Typeface to the CollapsingTextHelper TextPaint
            ((TextPaint) tpf.get(collapsingTextHelper)).setTypeface(tf);
        } catch (Exception ignored) {
            // Nothing to do
        }
    }

![](https://github.com/rathodchintan/TextInputLayout/blob/master/TextInputLayout%20Demo.gif)

