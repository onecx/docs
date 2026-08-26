# Replace PageContentComponent

In OneCX v6,

* Replace **PageContentComponent** with **OcxContentComponent** when **PageContentComponent** has title and styleClass
* Replace **PageContentComponent** with **OcxContentContainerComponent** when **PageContentComponent** is used for grouping multiple content sections together and support layout options.

## [](#%5Fcode%5Fchanges)Code Changes

* Remove `PageContentComponent` from `@onecx/portal-integration-angular`
* Add with `OcxContentComponent` from `@onecx/angular-accelerator`
* For grouping, Add with `OcxContentContainerComponent` from `@onecx/angular-accelerator`
* For single content sections, Replace tag `<ocx-page-content>` with `<ocx-content>`
* For grouping multiple content sections, Replace tag `<ocx-page-content>` with `<ocx-content-container>`
* Migrate input properties as per the mapping tables below

### [](#%5Fexamples)Examples

**Example: OcxContentComponent**.Before

```html
<ocx-page-content
  [styleClass]="'my-custom-class'"
>
  <!-- content here -->
</ocx-page-content>
```

After

```html
<ocx-content
  [styleClass]="'my-custom-class'"
  [title]="'My Page Title'"
>
  <!-- content here -->
</ocx-content>
```

**Example: OcxContentContainerComponent**

Before

```html
<h1>User Area</h1>
<page-content>
  <h1>Profile</h1>
  <app-profile-details></app-profile-details>
</page-content>
<page-content>
  <h2>Settings</h2>
  <app-settings-form></app-settings-form>
</page-content>
```

After

```html
<ocx-content-container [title]="'User Area'">
  <ocx-content [title]="'Profile'">
    <app-profile-details></app-profile-details>
  </ocx-content>
  <ocx-content [title]="'Settings'">
    <app-settings-form></app-settings-form>
  </ocx-content>
</ocx-content-container>
```

## [](#%5Fproperties%5Fmapping)Properties Mapping

__Table 1\. Input Properties__
| PageContentComponent | OcxContentComponent | Notes                                         |
| -------------------- | ------------------- | --------------------------------------------- |
| styleClass           | styleClass          | Indicates css class, applied to container div |
| \-                   | title               | (optional) Indicates the title of the content |

__Table 2\. Input Properties__
| PageContentComponent | OcxContentContainerComponent | Notes                                                                                                       |
| -------------------- | ---------------------------- | ----------------------------------------------------------------------------------------------------------- |
| styleClass           | styleClass                   | Indicates css class, applied to container div                                                               |
| \-                   | layout                       | Sets layout direction of container Values: vertical, horizontal Default value: vertical                     |
| \-                   | breakpoint                   | Sets breakpoint when horizontal layout switches to vertical layout Values: sm, md, lg, xl Default value: md |
