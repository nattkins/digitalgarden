---
{"dg-publish":true,"permalink":"/10212-search-ui/"}
---


Excerpt from the code that produces the results in search.
back to [[10212i documentation\|10212i documentation]]
[[10212a Search UI explained\|10212a Search UI explained]]

```<template id="content">

                    <li class="template--listItem">
                        {{#> resultTypes item=item}}
                        <div class="template--listItem--result {{#if (eq (segments (slot item @root.slots.Path) '4' '5') 'Insights')}}insight{{/if}}" >
                            {{#if @root.properties.layoutProperties.showFileIcon}}
                            {{#contains "['STS_Site','STS_Web']" (slot item @root.slots.contentclass)}}
                            <pnp-iconfile class="template--listItem--icon"
                                data-extension="{{slot item @root.slots.FileType}}"
                                data-is-container="{{slot item @root.slots.IsFolder}}"
                                data-image-url="{{item.SiteLogo}}" data-size="32"
                                data-theme-variant="{{JSONstringify @root.theme}}"></pnp-iconfile>
                            {{else}}
                            <pnp-iconfile class="template--listItem--icon"
                                data-extension="{{slot item @root.slots.FileType}}"
                                data-is-container="{{slot item @root.slots.IsFolder}}" data-size="32"
                                data-theme-variant="{{JSONstringify @root.theme}}"></pnp-iconfile>
                            {{/contains}}
                            {{/if}}
                            <div class="template--listItem--contentContainer">
                                <span class="template--listItem--title example-themePrimary">
                                    <a href="{{slot item @root.slots.PreviewUrl}}" target="_blank"
                                        style="color:{{@root.theme.semanticColors.link}}" data-interception="off"
                                        rel="noopener noreferrer">{{slot item @root.slots.Title}}</a>
                                </span>
                                <span>
                                    <span class="template--listItem--author">
                                        {{#with (split (slot item @root.slots.Author) '|')}}
                                        {{[1]}}
                                        {{/with}}
                                    </span>
                                    <span class="template--listItem--date">{{getDate (slot item @root.slots.Date)
                                        "LL"}}</span>
                                    {{#if (eq (segments (slot item @root.slots.Path) "4" "5") "Insights")}}
                                    <span class="template--listItem--author  ">{{decodeURI (segments (slot item
                                        @root.slots.Path) "5" "6")}}</span>
                                    {{/if}}
                                </span>
                                <div>{{getSummary (slot item @root.slots.Summary)}}</div>
                                <div class="template--listItem--tags example-themePrimary">
                                    {{#if (slot item @root.slots.Tags)}}
                                    <pnp-icon data-name="Tag" aria-hidden="true"
                                        data-theme-variant="{{JSONstringify @root.theme}}"></pnp-icon>
                                    <div>
                                        {{#each (split (slot item @root.slots.Tags) ",") as |tag| }}
                                        <span>{{trim tag}}</span>
                                        {{/each}}
                                    </div>
                                    {{/if}}
                                </div>
                                <div class="template--listItem--tags example-themePrimary">
                                    {{#if (slot item @root.slots.Stakeholders)}}
                                    <pnp-icon data-name="Tag" aria-hidden="true"
                                        data-theme-variant="{{JSONstringify @root.theme}}"></pnp-icon>
                                    <div>
                                        {{#each (split (slot item @root.slots.Stakeholders) ",") as |Stakeholder| }}
                                        <span>{{trim Stakeholder}}</span>
                                        {{/each}}
                                    </div>
                                    {{/if}}
                                </div>
                            </div>
                        </div>
                        {{#if @root.properties.layoutProperties.showItemThumbnail}}
                        <div class="template--listItem--thumbnailContainer" data-selection-disabled="true">
                            <div class="thumbnail--image">
                                <pnp-filepreview data-preview-url="{{slot item @root.slots.PreviewUrl}}"
                                    data-preview-image-url="{{slot item @root.slots.PreviewImageUrl}}"
                                    data-theme-variant="{{JSONstringify @root.theme}}">
                                    <pnp-img alt='preview-image' width="120"
                                        src="{{slot item @root.slots.PreviewImageUrl}}" loading="lazy"
                                        data-error-image="{{@root.utils.defaultImage}}" />
                                </pnp-filepreview>
                                <div class="thumbnail--hover">
                                    <div>
                                        <pnp-icon data-name="DocumentSearch" aria-hidden="true"></pnp-icon>
                                    </div>
                                </div>
                            </div>
                        </div>
                        {{/if}} {{/resultTypes}}
                    </li>
                </template>

```