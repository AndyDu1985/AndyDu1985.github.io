---
layout: post
title: All in english
---

```C#
        <Style x:Key="GroupHeaderStyle" TargetType="{x:Type GroupItem}">
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="{x:Type GroupItem}">
                        <Expander IsExpanded="True">
                            <Expander.Header>
                                <TextBlock Text="{Binding Path=Name}"/>
                            </Expander.Header>
                            <ItemsPresenter />
                        </Expander>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>
```

```javascript
/* Some pointless Javascript */
var rawr = ["r", "a", "w", "r"];
```
