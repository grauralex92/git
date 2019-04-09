# SmartCredentials Android Coding Standards

## 1. Code
### 1.1 File naming
Class names are written in __UpperCamelCase__.

For classes that extend an Android component, the name of the class should end with the name of the component. 
E.g.: 
`SignInActivity`, `SignInFragment`, `ImageUploaderService`, `ChangePasswordDialog`.

### 1.2 Style
Follow the official Android code style guidelines: [http://source.android.com/source/code-style.html](http://source.android.com/source/code-style.html)

### 1.3 Indentation
Use tab per indentation level and no whitespaces.

### 1.4 Line Length
Stick within the 120 char line limit. Use line breaks to split up code according to the style guidelines.

### 1.5 Whitespace
Code should not have any trailing whitespace to avoid creating unnecessary diff issues. Please setup your IDE to remove these as a save action.

### 1.6 Imports
#### 1.6.1 Unused imports
Please setup your IDE to remove all unused imports as a save action.

#### 1.6.2 Fully qualify imports
This is bad: `import foo.*;`

This is good: `import foo.Bar;`

## 2. XML

#### 2.1 File naming
Resources file names are written in __lowercase_underscore__. Unlike the rest of resources, style names are written in __UpperCamelCase__.

The Android build tools merge resources from a library module with those of a dependent app module.

To avoid resource conflicts for common resource IDs, use the following naming scheme, applying the `sc` prefix to resource namings:

##### 2.1.1 Drawable files

Naming conventions for drawables:

| Asset Type   | Prefix               |		Example                    | 
|------------- | -------------------- |------------------------------- |
| Action bar   | `sc_ab_`             | `sc_ab_stacked.9.png`          |
| Button       | `sc_btn_`	          | `sc_btn_send_pressed.9.png`    |
| Dialog       | `sc_dialog_`         | `sc_dialog_top.9.png`          |
| Divider      | `sc_divider_`        | `sc_divider_horizontal.9.png`  |
| Icon         | `sc_ic_`	          | `sc_ic_star.png`               |
| Menu         | `sc_menu_`           | `sc_menu_submenu_bg.9.png`     |
| Notification | `sc_notification_`	  | `sc_notification_bg.9.png`     |
| Tabs         | `sc_tab_`            | `sc_tab_pressed.9.png`         |

Naming conventions for icons:

| Asset Type                      | Prefix             	  | Example                         |
| ------------------------------- | --------------------- | ------------------------------- |
| Icons                           | `sc_ic_`              | `sc_ic_star.png`                |
| Launcher icons                  | `sc_ic_launcher`      | `sc_ic_launcher_calendar.png`   |
| Menu icons and Action Bar icons | `sc_ic_menu`          | `sc_ic_menu_archive.png`        |
| Status bar icons                | `sc_ic_stat_notify`   | `sc_ic_stat_notify_msg.png`     |
| Tab icons                       | `sc_ic_tab`           | `sc_ic_tab_recent.png`          |
| Dialog icons                    | `sc_ic_dialog`        | `sc_ic_dialog_info.png`         |

Naming conventions for selector states:

| State	       | Suffix          | Example                        |
|------------- |---------------- |------------------------------- |
| Normal       | `_normal`       | `sc_btn_order_normal.9.png`    |
| Pressed      | `_pressed`      | `sc_btn_order_pressed.9.png`   |
| Focused      | `_focused`      | `sc_btn_order_focused.9.png`   |
| Disabled     | `_disabled`     | `sc_btn_order_disabled.9.png`  |
| Selected     | `_selected`     | `sc_btn_order_selected.9.png`  |

##### 2.1.2 Layout files

Layout files should match the name of the Android components that they are intended for, but moving the top level component name to the beginning, after the library prefix. For example, if we are creating a layout for the `SignInActivity`, the name of the layout file should be `sc_activity_sign_in.xml`.

| Component        | Class Name             | Layout Name                      |
| ---------------- | ---------------------- | -------------------------------- |
| Activity         | `UserProfileActivity`  | `sc_activity_user_profile.xml`   |
| Fragment         | `SignUpFragment`       | `sc_fragment_sign_up.xml`        |
| Dialog           | `ChangePasswordDialog` | `sc_dialog_change_password.xml`  |
| AdapterView item | ---                    | `sc_item_person.xml`             |
| Partial layout   | ---                    | `sc_partial_stats_bar.xml`       |

##### 2.1.3 Menu files

Similar to layout files, menu files should match the name of the component. For example, if we are defining a menu file that is going to be used in the `UserActivity`, then the name of the file should be `sc_activity_user.xml`

A good practice is to not include the word `menu` as part of the name because these files are already located in the `menu` directory.

#### 2.2 Resources naming

Resource IDs and names are written in __lowercase_underscore__.

##### 2.2.1 ID naming

IDs should be prefixed with the libray prefix and then the name of the element in lowercase underscore. For example:

| Element              | Prefix                 |
| -------------------- | ---------------------- |
| `TextView`           | `sc_text_`             |
| `ImageView`          | `sc_image_`            |
| `Button`             | `sc_button_`           |
| `Menu`               | `sc_menu_`             |

Image view example:

	<ImageView
		android:id="@+id/sc_image_profile"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content" />

Menu example:

	<menu>
		<item
			android:id="@+id/sc_menu_done"
			android:title="Done" />
	</menu>

##### 2.2.2 Strings

String names start with the library prefix and a word that identifies the section they belong to. For example `sc_registration_email_hint` or `sc_registration_name_hint`. If a string __doesn't belong__ to any section, then you should follow the rules below:

| Prefix                  | Description                            |
| ----------------------- | -------------------------------------- |
| `sc_error_`             | An error message                       |
| `sc_msg_`               | A regular information message          |
| `sc_title_`             | A title, i.e. a dialog title           |
| `sc_action_`            | An action such as "Save" or "Create"   |
	
#### 2.3 Use self-closing tags
When an XML element doesn't have any content, you __must__ use self closing tags.

Do:

	<TextView
		android:id="@+id/text_view_profile"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content" />


Don't:

	<TextView
		android:id="@+id/text_view_profile"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content" >
	</TextView>

#### 2.3 Indentation
Use tab per indentation level and no whitespaces.  
Each attribute should appear on its own line.  
Add a space between the closing slash and the final attribute. E.g. ```android:textSize="10dp" />```

#### 2.4 Structure
As a general rule you should try to group similar attributes together. A good way of ordering the most common attributes is:

1. View Id
2. Style
3. Layout width and layout height
4. Other layout attributes, sorted alphabetically
5. Remaining attributes, sorted alphabetically

#### 2.5 IDE Auto format

Automatic formatting rules for our coding standards are stored in an Android Studio file inside the root of this repository. Please use File > Import Settings and select "android_studio_settings.jar" to ensure you get the same rules.

## Documentation

#### Javadoc
Any new classes that are committed must include a class descriptor Javadoc along with:
```@author name@address.com```
Javadoc any public methods, variables and constants. Javadoc private methods where beneficial.

#### Comments
Use in-line commenting to help the next developer who might be editing your code, even if it seems obvious now. Inline comments should appear on the line above the code your are commenting.
Comment XML View elements using ```<!-- Comment -->```.

## Version control
No commented out code must be committed unless you have a very good reason that is clearly described in a comment by the code you are ommitting.

For further details on branching strategies used at ustwo please see: [https://www.ustwo.com/blog/branching-strategies-with-git/](https://www.ustwo.com/blog/branching-strategies-with-git/)
