# HUBL

## Custom Header

``` html
{%- macro render_link_item(link,depth)-%}
{%- if link != [] && link.label -%}
    <li class="hs-menu-item hs-menu-depth-{{depth}} {{'hs-item-has-children' if link.children}}" aria-role="none" {{'aria-haspopup="true"' if link.children}}>
        <a href="{{link.url if link.url else '#'}}" aria-role="menuitem">{{link.label}}</a>
        {%- if link.children -%}
        <ul class="hs-menu-children-wrapper" aria-role="menu">
            {% set depth = depth + 1%}
            {%- for sublink in link.children -%}
            {{render_link_item(sublink,depth)}}
            {%- endfor -%}
        </ul>
        {%- endif -%}
    </li>
{%- endif -%}
{%- endmacro -%}
<nav class="sc-site-header__menu sc-site-header__menu--{{ module.menu_field }} hs-menu-wrapper active-branch flyouts hs-menu-flow-horizontal" aria-label="{{menu_name}} menu">
    {% set menu = menu(module.menu_field , "site_root").children %}
    <ul aria-role="menubar">
        {% for link in menu %}
        {{render_link_item(link,1)}}
        {% endfor %}
    </ul>
</nav>
```

## Custom HubSpot form module
``` html
{% form
    form_to_use="{{ module.form.form_id }}"
    title="{{ module.title }}"
    no_title="{{ module.add_title }}"
    response_response_type="{{ module.form.response_type }}"
    response_message="{{ module.form.message }}"
    response_redirect_id="{{ module.form.redirect_id }}"
    response_redirect_url="{{module.form.redirect_url}}"
    gotowebinar_webinar_key="{{ module.form.gotowebinar_webinar_key }}"
    notifications_are_overridden='{{ module.notifications_are_overridden }}'
    notifications_override_email_addresses='{{ module.notifications_override_email_addresses }}'
    follow_up_type_simple='{{ module.follow_up_type_simple }}'
    simple_email_for_live_id='{{ module.simple_email_for_live_id }}'
%}
```
Fields :
* Form | form | form field
* Add a title? | add_title | boolean field
* Form title | title | text field
* Send form notifications to specified email addresses instead of the form defaults | notifications_are_overridden | boolean field
* Email address | notifications_override_email_addresses | email address field 
* Send a follow-up email | follow_up_type_simple | boolean field
* Email | simple_email_for_live_id | followup email field