---
layout: post
title: "Add Gift Notes to Your Shopify Store"
date: 2024-10-23
image: "/img/blog/gift-note/gift-note-for-theme.png"
author: Katrina
---
{% raw  %}

<br/>
Add individual gift notes to your products, without using any apps.

## Order notes vs. individual gift note

By default, many Shopify themes give an option for Order Notes on cart checkout, which will attach a note to the entire order. For example, see the "Order Special Instructions" box here:

![Order note example](/img/blog/gift-note/order-notes.png)

This has a couple of drawbacks for a flower shop:

- This is not intuitive for the customer. You often need to add extra instructions to tell the customer when and where they can write a gift note.
- If there are multiple arrangements in an order, there will still only be one cart note.
- This box is not just used for gift notes but also design preferences and other instructions.

In this post, we’ll go over how to add a gift note to individual products to give customers a better experience. By the end of this blog, you'll have something like this on your product pages:

![Gift note example](/img/blog/gift-note/gift-note-for-theme.png)

It's quite simple and you can do it without any apps! You will need a little code, but we’ll walk you through it. **Note that we are using Google Chrome for our web browser, which is relevant for Step 3.**

## Step 1: Find the Product page in your theme editor

Navigate to the “Customize” button of your theme editor on the “Themes” screen

![Open theme editor](/img/blog/gift-note/theme-editor.png)

Navigate to your product page:

![Navigate to your product page](/img/blog/gift-note/product-nav.png)

## Step 2: Create the gift note block on the page

Find the section that says "Product Information." Click "Add block," and choose "Custom Liquid."

![Add block](/img/blog/gift-note/add-block.png)

Add this custom liquid code:

```html
<textarea id="giftnote" placeholder="Gift Note" name="properties[giftnote]"></textarea>
```

Drag and drop your “Custom Liquid” block to the desired place on your product page. We’ve added it after the Quantity selector below.

![Custom liquid](/img/blog/gift-note/custom-liquid.png)

Yay, we’ve added a Gift Note to the page! We still need to link it to the order form so that the note is linked to the product when it’s added to the cart.

## Step 3: Link the gift note to the order form

Now we have to edit the “Custom Liquid” block you just made so it links to the form. To do this, we need to find the generic form ID for your theme.

If you’re using **Dawn** or **Sense**, then you can luckily skip this step! We've found the generic form ID, so you can update your "Custom Liquid" with the attribute `form="product-form-{{ section.id }}"` so it looks like this:

```html
<textarea id="giftnote" placeholder="Gift Note" name="properties[giftnote]" form="product-form-{{ section.id }}"></textarea>
```

Then skip to Step 4. If you're using a different theme, let's find the generic form ID together.

### Find the theme's generic form ID:

In a separate window, open a product page on your website. Right-click on your “Add to Cart” button and select "Inspect".
    ![Inspect Add to Cart button](/img/blog/gift-note/inspect-add-to-cart.png)
This will open Google Chrome's Web Inspector. Don’t be intimidated, we’ll go over it together. We’re going to look at a couple of elements:
    ![Investigate HTML](/img/blog/gift-note/investigate-html.png)

1. **Look for the product submit button (A):** You’ll see a line highlighted when it opens. We’ll call this A and use it to orient ourselves.
2. **Look for the add to cart form (B):** Now look at the lines above A until you find a `<form>` element, which we’ll call B.
3. **On B, get the form ID for the page:** This line begins with `<form …>`. It should have `action=“/cart/add”`. Look to the right and find the attribute `id`. In this case, you can see `id="product-form-template-16090539327572_main"`.  

    Okay, great! We have a form ID for the page: `product-form-template-16090539327572_main`. But this is the form ID for only this product, and we need a generic ID that will work for all products with a gift note.
4. **Look for product-id and section-id (C):** Now go back to A and look below it. You will see two lines that begin with `<input ...>`. One of them will have `name=”product-id”` and one will have `name=”section-id”`. We’ll call these two lines C.
5. **On C, check the product-id and section-id:** Look at the “value” fields. See which one matches the end of our form ID for the page. In our example:
    - For product-id, the value is `"7537494655060"`.
    - For section-id, value is`"template-16090539327572_main"`.
    
    Since the section-id is a match, the generic form ID is `product-form-{{ section.id }}`.

### Update the Custom Liquid with the generic form ID.
Now that we have the form ID, go back to the "Custom Liquid" block you made in Step 2. Update the attribute `form="product-form-{{ section.id }}"` so it looks like this:

```html
<textarea id="giftnote" placeholder="Gift Note" name="properties[giftnote]" form="product-form-{{ section.id }}"></textarea>
```

## Step 4: Test it!

Your gift note should work now. Try adding an arrangement to your cart, and check your cart. You should see a gift note for the product.

![Test your gift note](/img/blog/gift-note/test-message.png)

## Step 5: Make it pretty (optional)

You can modify the classes in your Custom Liquid so that the Gift Note matches your theme. This step is totally optional.

Before making it pretty:
![Gift note plain](/img/blog/gift-note/gift-note-plain.png)


After making it pretty:
![Gift note styling](/img/blog/gift-note/gift-note-for-theme.png)

And we're done!

## Recap

The finished code (for Dawn and Sense):

```html
<textarea id="giftnote" placeholder="Gift Note" name="properties[giftnote]" form="product-form-{{ section.id }}"></textarea>
```

Finished code with styling (for Sense):

```html
<div class="field">
  <textarea class="field__input text-area" id="giftnote" placeholder="Gift Note" name="properties[Gift Note]" form="product-form-{{ section.id }}"></textarea>
  <label class="form__label field__label" for="giftnote">Gift Note</label>
</div>
```

---

## Enhance your website with Foxtail

At **Foxtail**, we understand how crucial your website is for your business. We also know you're passionate about flowers, not technology. That's why we create tools that are simple to integrate into your website—no tech experience needed. Our first product, a free Shopify app, lets you set up a custom bouquet feature in under two minutes. New exciting tools are in the works, so [sign up for our mailing list](#) to keep up with the latest news!

{% endraw  %}