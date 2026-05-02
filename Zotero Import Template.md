---
Title: 
- {% if title %}{{title | replace('`', '') | replace('[', '') | replace(']', '')}}{% endif %}


citekey: {{citationKey}}



{%- if itemType == "interview" %}
{%- if creators.length > 0 %}
interviewee:
{%- for creator in creators %} 
{%- if creator.creatorType == "interviewee" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %} 
{%- endfor %}
interviewer:
{%- for creator in creators %} 
{%- if creator.creatorType == "interviewer" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %} 
{%- endfor %}
{%- endif %}
{%- else %}
{%- if itemType == "instantMessage" %}
participants:
{%- if creators.length > 0 %}
{%- for creator in creators %} 
{%- if creator.creatorType == "author" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %} 
{%- endfor %}
{%- endif %}
{%- else %}
Authors: 
{%- if creators.length > 0 %}
{%- for creator in creators %} 
{%- if creator.creatorType == "author" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %} 
{%- if creator.creatorType == "editor" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %}
{%- if creator.creatorType == "director" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %}
{%- if creator.creatorType == "contributor" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %}
{%- if creator.creatorType == "producer" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %}
{%- if creator.creatorType == "castMember" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %}
{%- if creator.creatorType == "producer" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %}
{%- if creator.creatorType == "presenter" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %}
{%- endfor %}
{%- endif %}
{%- if itemType == "email" %}
{%- if creators.length > 0 %}
contributor:
{%- for creator in creators %} 
{%- if creator.creatorType == "contributor" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %} 
{%- endfor %}
recipient:
{%- for creator in creators %} 
{%- if creator.creatorType == "recipient" %} 
- {% if creator.name %}"[[{{creator.name}}]]"{% else %}"[[{{creator.firstName}} {{creator.lastName}}]]"{% endif %}
{%- endif %} 
{%- endfor %}
{%- endif %}
{%- endif %}
{%- endif %}
{%- endif %}
{% if date %}
date: {{date | format ("YYYY")}}
{%- if itemType == "email" %}{%- endif %}

{%- else %}




{%- endif %}
{%- if publicationTitle %}
Publication: "[[{{publicationTitle| replace(':', '')}}]]"
{%- elseif seriesTitle %}
Publication: "[[{{seriesTitle| replace(':', '')}}]]"
{%- elseif bookTitle %}
Publication: "[[{{bookTitle| replace(':', '')}}]]"
{%- elseif forumTitle %}
Publication: "[[{{forumTitle| replace(':', '')}}]]"
{%- endif %}
{%- if itemType == "journalArticle" %}


{%- endif %}




{% if ISBN %}
ISBN: {{ISBN}}
{%- endif %}

{% if DOI %}
DOI: https://doi.org/{{DOI}}
{%- endif %}




{% if publisher %}
Publisher: {{publisher}}
{%- endif %}

{% if university %}
University: {{university}}
{%- endif %}


Zotero: {{desktopURI}}
{%- if relations.length >0 %}

{%- endif %}








PDF: "{{pdfLink}}"



tags: 
- {{itemType}} 
-  {{presenters}} 

Read?: false
---

{% persist "notes" %}

## <font color="#ee795e">Introduction</font>




## Notes



>[!summary]+ Summary
>- Main Findings/Thesis/Argument:
>- Implications:
>- Limitations:
>- Future work:

{% if annotations.length > 0 -%}

## Attachment Annotations
{%- endif %} 
{% for annotation in annotations -%}
{%- if annotation.comment -%}
{%- if annotation.annotatedText %}
<span style="background-color:{{annotation.colorCategory}};color:Black">✎</span> **{{annotation.colorCategory}} {{annotation.type | capitalize}}** - {% if pdfLink %}[{% if annotation.page %}Page {{annotation.page}}{%- else %}Page 1{% endif %}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}}){% else %}[{% if annotation.page %}Page {{annotation.page}}{%- else %}Position{% endif %}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}}){% endif %}

{%- if annotation.tags.length > 0 %}

{% for antag in annotation.tags %}#{{antag.tag}} {% endfor %}

{%- endif %}

> {{annotation.annotatedText | escape }} 

**Note:** {{annotation.comment}} 


---
{% endif -%}
{%- endif -%}

{% if annotation.imageRelativePath %} 
📊 **Image** - {% if pdfLink %}[{% if annotation.page %}Page {{annotation.page}}{%- else %}Page 1{% endif %}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}}){% else %}[{% if annotation.page %}Page {{annotation.page}}{%- else %}Position{% endif %}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}}){% endif %}

{%- if annotation.tags.length > 0 %}

{% for antag in annotation.tags %}#{{antag.tag}} {% endfor %}

{%- endif %}

> ![[{{annotation.imageRelativePath}}]]

{%- if annotation.comment %} 

**Note:** {{annotation.comment}} 
{%- endif %}

---
{% endif -%}

{% if annotation.type == "note" %} 
<span style="background-color:{{annotation.colorCategory}};color:Black">⚑</span> **{{annotation.colorCategory}} {{annotation.type | capitalize}}** - {% if pdfLink %}[{% if annotation.page %}Page {{annotation.page}}{%- else %}Page 1{% endif %}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}}){% else %}[{% if annotation.page %}Page {{annotation.page}}{%- else %}Position{% endif %}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}}){% endif %}

{%- if annotation.tags.length > 0 %}

{% for antag in annotation.tags %}#{{antag.tag}} {% endfor %}

{%- endif %}

{%- if annotation.comment %} 

**Note:** {{annotation.comment}} 
{%- endif %}

---
{% endif -%}
{%- endfor -%}
{% endpersist %}