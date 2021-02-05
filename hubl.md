# HUBL

## Custom Langage Switcher (Only for pages, not for blog)

```html
<ul>
    <li><a href="/{{ content.slug }}">{{ content.slug }}</a></li>
    <li><a href="/{{ content.translated_content['en'].slug || 'en' }}">{{ content.translated_content['en'].slug || en }}</a></li>
    <li><a href="/{{ content.translated_content['fr'].slug || 'fr' }}">{{ content.translated_content['fr'].slug || fr }}</a></li>
</ul>
```

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

## Custom Form Resubmit
``` css
<style>
form.hs-form.has-resub {
    position: relative;
}
form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex !important; /* because hubspot inline style */
    justify-content: center;
    align-items: center;
    z-index: 20;
    background-color: rgba(255,255,255, 0.75);
}
form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] a,
form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] label {
    display: block;
    font-size: 2rem;
    line-height: 1.75;
    padding: 1rem;
    text-align: center;
    color: #635a79;
}
.blog-logo-menu-module .newsletter-container {
    position: relative;
}
.blog-logo-menu-module form.hs-form.has-resub {
    position: unset;
}
.blog-logo-menu-module form.hs-form.has-resub .field,
.footer-module form.hs-form.has-resub .field {
    position: unset;
}
.blog-logo-menu-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] {
    top: 50%;
    height: 110px;
    background-color: rgba(99, 90, 121, 0.85);
    box-shadow: unset;
    padding-left: 1rem;
    transform: translate(0,-50%);
}
.blog-logo-menu-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] a,
.blog-logo-menu-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] label {
    color: #FFF;
}
.footer-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] {
    background-color: rgba(234, 234, 234, 0.85);
    padding-left: 0rem;
}
.blog-logo-menu-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] a,
.footer-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] a,
.blog-logo-menu-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] label,
.footer-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] label {
    font-size: 1.2rem;
    line-height: 1.5;
}
</style>
```
```javascript
<script>
    document.addEventListener('DOMContentLoaded', () => {
        const currentForms = document.querySelectorAll('.hs_cos_wrapper_type_form')
        let formCount = currentForms.length;
        window.addEventListener('message', event => {
            if(event.data.type === 'hsFormCallback' && event.data.eventName === 'onFormReady') {
                formCount--;
                if (formCount === 0) {
                    const forms = document.querySelectorAll('form.hs-form');
                    forms.forEach(form => {
                    const ulError = form.querySelector('ul.no-list.hs-error-msgs.inputs-list[role="alert"]');
                    if (ulError) {
                        const tempErrorLink = (ulError.querySelector('a') || ulError.querySelector('label'));
                        if (tempErrorLink && (tempErrorLink.textContent === "Vous avez demandé à ce que des notifications ne vous soient plus envoyées par e-mail. Cliquez ici pour recevoir un e-mail vous permettant d'en bénéficier à nouveau." || tempErrorLink.textContent === "Consultez votre boîte de réception pour recevoir à nouveau des notifications.")) {
                        form.classList.add('has-resub');
                        }
                    }
                    // Selectionne le noeud dont les mutations seront observées
                    const targetNode = form;
                    // Options de l'observateur (quelles sont les mutations à observer)
                    const config = { attributes: true, childList: true };
                    // Fonction callback à éxécuter quand une mutation est observée
                    const callback = function(mutationsList) {
                        for(var mutation of mutationsList) {
                        if (mutation.type == 'childList') {
                            // console.log('Un noeud enfant a été ajouté ou supprimé.');
                            const currentError = document.querySelector('form.hs-form ul.no-list.hs-error-msgs.inputs-list[role="alert"]');
                            if (currentError) {
                            const currentErrorLink = (currentError.querySelector('a') || currentError.querySelector('label'));
                            if (currentErrorLink && (currentErrorLink.textContent === "Vous avez demandé à ce que des notifications ne vous soient plus envoyées par e-mail. Cliquez ici pour recevoir un e-mail vous permettant d'en bénéficier à nouveau." || currentErrorLink.textContent === "Consultez votre boîte de réception pour recevoir à nouveau des notifications.")) {
                                form.classList.add('has-resub');
                            } else {
                                form.classList.remove('has-resub');
                            }
                            }
                        }
                        {#
                        else if (mutation.type == 'attributes') {
                            console.log("L'attribut '" + mutation.attributeName + "' a été modifié.");
                        }
                        #}
                        }
                    };
                    // Créé une instance de l'observateur lié à la fonction de callback
                    const observer = new MutationObserver(callback);
                    // Commence à observer le noeud cible pour les mutations précédemment configurées
                    observer.observe(targetNode, config);
                    })
                }
            }
        })
    })
</script>
```