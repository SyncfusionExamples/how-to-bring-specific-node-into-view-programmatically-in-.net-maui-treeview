# how-to-bring-specific-node-into-view-programmatically-in-.net-maui-treeview
This repository demonstrates how to programmatically bring a specific node into view in the .NET MAUI TreeView (SfTreeView) control. It provides a sample implementation using a custom behavior and the BringIntoView method, allowing you to scroll and focus on a particular node in response to user actions or application logic.

## Sample

### XAML

```xaml

<ContentPage.Behaviors>
    <local:BringIntoViewBehavior/>
</ContentPage.Behaviors>
    
<ContentPage.Content>
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
        <Button x:Name="bringIntoView" Text="BringIntoView" HeightRequest="50" Grid.Row="0" HorizontalOptions="Center" BackgroundColor="Violet" />
        <syncfusion:SfTreeView x:Name="treeView" Grid.Row="1"
                                   AutoExpandMode="RootNodesExpanded"
                                   ChildPropertyName="SubFiles"
                                   ItemTemplateContextType="Node"                           
                                   ItemsSource="{Binding ImageNodeInfo}" >
        </syncfusion:SfTreeView>
    </Grid>
</ContentPage.Content>
```

### Behavior

```csharp
internal class BringIntoViewBehavior : Behavior<ContentPage>
{
    #region Fields

    private SfTreeView TreeView;
    private Button Button;
    #endregion

    #region Overrides
    protected override void OnAttachedTo(ContentPage bindable)
    {
        TreeView = bindable.FindByName<SfTreeView>("treeView");
        Button = bindable.FindByName<Button>("bringIntoView");
        Button.Clicked += BringIntoView_Clicked;

        base.OnAttachedTo(bindable);
    }

    protected override void OnDetachingFrom(ContentPage bindable)
    {
        Button.Clicked -= BringIntoView_Clicked;
        Button = null;
        TreeView = null;
        base.OnDetachingFrom(bindable);
    }

    #endregion

    #region CallBack
    private void BringIntoView_Clicked(object sender, EventArgs e)
    {
        var viewModel = TreeView.BindingContext as FileManagerViewModel;
        var count = viewModel.ImageNodeInfo.Count;
        var data = viewModel.ImageNodeInfo[count - 1];
        TreeView.BringIntoView(data);
    }
    #endregion
}
```

## Requirements to run the demo

To run the demo, refer to [System Requirements for .NET MAUI](https://help.syncfusion.com/maui/system-requirements).

Make sure that you have the compatible versions of [Visual Studio 2022](https://visualstudio.microsoft.com/downloads/ ) with the Dot NET MAUI workload and [.NET Core SDK 7.0](https://dotnet.microsoft.com/en-us/download/dotnet/7.0) or later version in your machine before starting to work on this project.

## Troubleshooting:
### Path too long exception

If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.

## License

Syncfusion® has no liability for any damage or consequence that may arise from using or viewing the samples. The samples are for demonstrative purposes. If you choose to use or access the samples, you agree to not hold Syncfusion® liable, in any form, for any damage related to use, for accessing, or viewing the samples. By accessing, viewing, or seeing the samples, you acknowledge and agree Syncfusion®'s samples will not allow you seek injunctive relief in any form for any claim related to the sample. If you do not agree to this, do not view, access, utilize, or otherwise do anything with Syncfusion®'s samples.
