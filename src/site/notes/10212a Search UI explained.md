---
{"dg-publish":true,"permalink":"/10212a-search-ui-explained/"}
---


[[10212 UKPN Insight Hub\|10212 UKPN Insight Hub]]

Most of the code is there by default I'll explain where I have altered it, and in most cases this is to achieve the different appearance of the search results for insight documents, those in the insight library

## General comments about Handlebars 
>yYes - like a moustache, in more ways than one. I've a funny story about this - I had an interview once that went wrong , when I asked which template engine I preferred I replied Handlebars, the interview asked why and I answered 'Because its Movember?' (you had to be there) - LSS don't work with people with no sense of humour.

This code uses handlebars helpers documented here https://github.com/helpers/handlebars-helpers

```
{{#if (eq (segments (slot item @root.slots.Path) '4' '5') 'Insights')}}insight{{/if}}
```

This uses the [segments](https://github.com/helpers/handlebars-helpers?tab=readme-ov-file#segments) helper that reads the 'Path ' which within the PNP search webpart is mapped to the DefaultEncodingURL filepath that contains the file path and looks between the 4 and 5 back slashes for the word insight, as can be seen for each file in the details panel for each section like this.

![pics/Screenshot 2024-03-18 at 23.51.18.png](/img/user/pics/Screenshot%202024-03-18%20at%2023.51.18.png)
and the URL looks like 

```
https://ukpowernetworks.sharepoint.com/sites/InsightsHubTest/Insights/Innovations/Net%20Zero/Appendix-21c-DFES-stakeholder-reports.pdf
```

WARNING 
this is not the same thing as the copy link that's some odd thing that only makes sense to SharePoint.





Line 4 identifies that a search result is from the insights library and assigns the CSS class "Insights" so that's how the boxes works 


```.insight {
            border: 1px solid rgb(247, 145, 43);
            background-color: rgb(248, 235, 220);
            padding:8px;
        }

```

Line 33 Makes sure that for insight items the department name is displayed next to the date , which uses the same Segments trick once to identify that file is an insights document and the second to find the following slash, which because of the folder structure gives us our department name. (cute right?)

Lines 40 through 49 and 50 through 59 are identical in that they display the metadata 'tags' associated with Tags which is a slot name mapped to - here is a screenshot showing the slot configuration 


![Screenshot 2024-03-19 at 00.02.14.png](/img/user/pics/Screenshot%202024-03-19%20at%2000.02.14.png)

Refineablestring01 and Refineablestring02 are created as managed crawled properties and the best description of setting them up is in the video here [[10212 X managed crawled properties\|10212 X managed crawled properties]] 

line 40 and 50 check that a value is present

```
{{#if (slot item @root.slots.Tags)}}

```

And if nothing doing - do nothing.

then line 52 is show the tag icon 

then 
```
{{#each (split (slot item @root.slots.Stakeholders) ",") as |Stakeholder| }}
<span>{{trim Stakeholder}}</span>
{{/each}}
```

Because these two metadata fields may contain multiple values its necessary to split them , trim them of spaces and display each one in its own span tag.

