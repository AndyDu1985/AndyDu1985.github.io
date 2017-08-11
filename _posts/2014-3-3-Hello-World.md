---
layout: post
title: Hello world!
---

Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).

效果如图，每个列的名字可以自定义。我随便用了"File"和"Attachment Name"。
![这里写图片描述](http://img.blog.csdn.net/20170215151753573?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYW55aWNoZW5nMjAxNQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

在Window的Resources里面设置Style, GroupHeaderStyle：
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
把这个Style应用到DataGrid上面：
```C#
            <DataGrid.GroupStyle>
                <GroupStyle ContainerStyle="{StaticResource GroupHeaderStyle}">
                    <GroupStyle.Panel>
                        <ItemsPanelTemplate>
                            <DataGridRowsPresenter/>
                        </ItemsPanelTemplate>
                    </GroupStyle.Panel>
                </GroupStyle>
            </DataGrid.GroupStyle>
```
整体xaml文件：
```C#
<Window x:Class="DataGridGroupDeamon.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="350" Width="525">
    <Window.Resources>
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
    </Window.Resources>
    <Grid>
        <DataGrid x:Name="dataGrid1"  AutoGenerateColumns="False" Margin="10">
            <DataGrid.GroupStyle>
                <GroupStyle ContainerStyle="{StaticResource GroupHeaderStyle}">
                    <GroupStyle.Panel>
                        <ItemsPanelTemplate>
                            <DataGridRowsPresenter/>
                        </ItemsPanelTemplate>
                    </GroupStyle.Panel>
                </GroupStyle>
            </DataGrid.GroupStyle>

            <DataGrid.Columns>
                <DataGridTextColumn Header="File" Binding="{Binding Name}"/>
                <DataGridTextColumn Header="Attachment Name" Binding="{Binding Sex}"/>

            </DataGrid.Columns>
        </DataGrid>
    </Grid>
</Window>

```
数据准备文件：
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
using System.Collections.ObjectModel;
using System.ComponentModel;

namespace DataGridGroupDeamon
{
    /// <summary>
    /// MainWindow.xaml 的交互逻辑
    /// </summary>
    public partial class MainWindow : Window
    {
        ObservableCollection<Model> data = new ObservableCollection<Model>();

        public MainWindow()
        {
            InitializeComponent();

            dataGrid1.ItemsSource = data;
            for (int i = 0; i < 10; i++)
            {
                Model m = CreateModel("张" + i, i / 2 + "年级", (i % 2 == 0 ? "女" : "男"));
                data.Add(m);
            }
            ICollectionView vw = CollectionViewSource.GetDefaultView(data);
            vw.GroupDescriptions.Add(new PropertyGroupDescription("Category")); 
        }

        private Model CreateModel(string name, string cate, string sex)
        {
            Model model = new Model();
            model.Name = name;
            model.Category = cate;
            model.Sex = sex;
            return model;
        }
    }

    public class Model
    {
        public string Name
        {
            get;
            set;
        }

        public string Category
        {
            get;
            set;
        }

        public string Sex
        {
            get;
            set;
        }
    }
}

```
