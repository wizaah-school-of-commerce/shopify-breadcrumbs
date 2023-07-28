# Shopify Breadcrumbs

Breadcrumbs are an essential navigation aid that helps visitors understand their current location within your website's hierarchy and allows them to navigate back to parent pages easily.


## Installation

Follow these simple steps to add this breadcrumbs solution to your store:

1. **Access Theme Code Editor**: 
    Login to your Shopify admin panel and navigate to <br /> `Online Store` > `Themes` > `Edit code`

2. **Add Breadcrumbs Code**: Create a snippet named `breadcrumbs.liquid` under `Snippets` and paste the below code into that file.


```liquid

{% style %}
  .breadcrumbs__list {
    margin: 0;
    padding: 0;
    display: flex;
    list-style-type: none;
  }

  .breadcrumbs__listitem {
    display: flex;
  }

  .breadcrumbs__listitem:not(:first-child)::before {
    content: '/';
    padding: 0 8px;
  }

  .breadcrumbs__link {
    color: inherit;
    text-decoration: none;
  }

  .breadcrumbs__link:not([aria-current='page']) {
    font-weight: bold;
  }
{% endstyle %}

{%- unless template == 'index' or template == 'cart' or template == '404' -%}
  {%- assign template_name = template | split: '.' | first -%}

  <nav class="breadcrumbs" role="navigation" aria-label="breadcrumbs">
    <ol class="breadcrumbs__list">
      <li class="breadcrumbs__listitem">
        <a class="breadcrumbs__link" href="{{ routes.root_url }}" title="Home">Home</a>
      </li>

      {%- case template_name -%}
        {%- when 'collection' and collection.handle -%}
          <li class="breadcrumbs__listitem">
            <a class="breadcrumbs__link" href="{{ collection.url }}" aria-current="page">{{ collection.title }}</a>
          </li>
        {%- when 'product' -%}
          {%- if collection and collection.url -%}
            <li class="breadcrumbs__listitem">
              <a class="breadcrumbs__link" href="{{ collection.url }}">{{ collection.title }}</a>
            </li>
          {%- endif -%}

          <li class="breadcrumbs__listitem">
            <a class="breadcrumbs__link" href="{{ product.url }}" aria-current="page">{{ product.title }}</a>
          </li>
        {%- when 'blog' -%}
          <li class="breadcrumbs__listitem">
            <a class="breadcrumbs__link" href="{{ blog.url }}" aria-current="page">{{ blog.title }}</a>
          </li>
        {%- when 'article' -%}
          <li class="breadcrumbs__listitem">
            <a class="breadcrumbs__link" href="{{ blog.url }}" aria-current="page">{{ blog.title }}</a>
          </li>
          <li class="breadcrumbs__listitem">
            <a class="breadcrumbs__link" href="{{ article.url }}" aria-current="page">{{ article.title }}</a>
          </li>
        {%- when 'page' -%}
          <li class="breadcrumbs__listitem">
            <a class="breadcrumbs__link" href="{{ page.url }}" aria-current="page">{{ page.title }}</a>
          </li>
        {%- else -%}
          <li class="breadcrumbs__listitem">
            <a class="breadcrumbs__link" href="{{ request.path }}" aria-current="page">{{ page_title }}</a>
          </li>
      {%- endcase -%}
    </ol>
  </nav>
{%- endunless -%}

```

3. **Place Breadcrumbs Snippet**: Open the `theme.liquid` file from `Layout` folder, and add <br /> `{% render 'breadcrumbs' %}` wherever you wish the breadcrumb to appear.

4. **Save Changes**: Save the changes.

5. **Preview and Change**: Go to your storefront and navigate through different pages to see the breadcrumbs.
   

## Note

> This solution provides basic styling to get you started quickly. However, you have complete freedom to customize the breadcrumbs according to your specific needs and design preferences. Feel free to modify the CSS properties within the code snippet to change colors, spacing, and other stylistic elements.