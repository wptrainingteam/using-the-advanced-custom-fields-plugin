# Using The Advanced Custom Fields Plugin

## Description

Advanced Custom Fields (ACF for short) is a plugin that allows you to create _custom field groups_ for posts, pages, or custom post types. It provides a graphical user interface to add a variety of different field types including text fields, WYSIWYG areas, checkboxes, radio buttons, and more. In this lesson you'll learn how to set up the ACF plugin, how to create a custom field group for a custom post type, and how to display this information to a site visitor.

## Prerequisite Skills

*   [Ability to install a plugin](https://make.wordpress.org/training/handbook/lesson-plans/user-lessons/choosing-and-installing-plugins/)
*   An understanding of [post types](https://make.wordpress.org/training/handbook/lesson-plans/theme-school/custom-post-types/) and [taxonomies](https://codex.wordpress.org/Taxonomies)
*   Ability to create [a child theme](https://make.wordpress.org/training/handbook/lesson-plans/theme-school/child-themes/) and [a custom post type](https://make.wordpress.org/training/handbook/lesson-plans/theme-school/custom-post-types/)

## Objectives

*   Students will be able to add custom fields to a custom post type and style the data stored in these fields in a custom theme template.

## Assets

*   [Advanced Custom Fields plugin](https://wordpress.org/plugins/advanced-custom-fields/)
*   Installation of WordPress
*   [The Twenty Sixteen theme](https://wordpress.org/themes/twentysixteen/)

## Screening Questions

*   Have you created content on a WordPress site?
*   Are you familiar with installing plugins?
*   Have you created a child theme?
*   Have you created a custom post type?
*   Are you comfortable editing theme templates?

## Teacher Notes

*   Performing a live demonstration of identifying and installing the plugin from WordPress.org.
*   It is easiest for students to work on a locally installed copy of WordPress. Set some time aside before class to help students with installing WordPress locally if they need it. For more information on how to install WordPress locally, please visit our [Teacher Resources page](https://make.wordpress.org/training/teacher-resources/).
*   The preferred answer to the screening questions is “yes.” Participants who reply “no” to the screening questions may need more hands on guidance for this lesson, however they should be able to learn based on code samples etc.

## Hands On Walkthrough

### Introduction: What Is Advanced Custom Fields?

Welcome to Advanced Custom Fields! Today you are going to learn how to use this popular plugin - with over a million active installs - to extend WordPress' customizability.

Once you learn how to manipulate content on your WordPress site and create [custom post types](https://codex.wordpress.org/Post_Types), you’ll often want to extend the content storage capabilities of WordPress by creating custom fields. [Advanced Custom Fields](https://wordpress.org/plugins/advanced-custom-fields/) provides a graphical user interface (GUI) for doing exactly that. This combination of custom post types and custom fields is what make WordPress a popular and full-featured content management system.

ACF offers the following benefits:

*   **Field validation**: Certain types of fields, such as email, are validated to be sure they’re entered correctly.
*   **Flexibility:** A wide selection of field types, including text fields, WYSIWYGs, file and image inputs, and several ways to reference other content on your WordPress site. Additionally, ACF provides some specialized field types that rely on jQuery: Google Maps, Date Picker, and Color Picker.
*   **Portability**: Field groups can be exported and imported, and even converted into PHP code for inclusion into your custom theme or plugin, allowing them to be reused in different projects and managed in version control.

In this lesson, you will build a WordPress site for a mythical company, YayWP!. In addition to the default “page” and “post” post types, you’ll display the company’s employees on the site via a custom post type, complete with their job titles and start dates. Some of the native fields can be repurposed, but others will need to be created, and that’s where Advanced Custom Fields comes in.

### Step 1: Create a Child Theme

Build a child theme from the Twenty Sixteen default theme. For now, create the **style.css** file and **functions.php** with the minimum needed to be recognized as a theme in the “Appearance” administration screen. If you need help, you can refer to the [Child Themes page in the WordPress Codex](https://codex.wordpress.org/Child_Themes).

Activate the child theme.

### Step 2: Create a Custom Post Type for Employees

Using either a plugin like Custom Post Type UI or edit the **functions.php** file in your child theme, create the custom post type with the key “employee”. Here is the code to use in **functions.php**:

```PHP
/**
 * Create a custom post type for employee information
 */

function employee_cpt() {
  $args = array(
    'labels'        => array(
      'name'          => _x( 'Employees', 'post type general name', 'twentysixteen-child' ),
      'singular_name' => _x( 'Employee', 'post type singular name', 'twentysixteen-child' )
    ),
    'description'   => __( 'Employee information.', 'twentysixteen-child' ),
    'public'        => true,
    'supports'      => array( 'title', 'editor', 'thumbnail' ),
    'menu_icon'     => 'dashicons-groups'
  );
  register_post_type( 'employee', $args );
}

add_action( 'init', 'employee_cpt' );
```

<img class="alignnone wp-image-5636 size-large" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_02_PM-1024x819.png" alt="2_1_16__10_02_PM" width="632" height="505" />

Via the Dashboard, navigate to “Settings” → “Permalinks” and choose a common permalink setting, then click “Save Changes”. <em>You **must** click “Save Changes”, even if you have not made any changes to your permalink settings, in order for WordPress to recognize posts with your new custom post type.</em>

<img class="alignnone size-large wp-image-5645" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_53_PM-1024x699.png" alt="2_1_16__10_53_PM" width="632" height="431" />

### Step 3: Install the Advanced Custom Fields Plugin

Via the Dashboard, navigate to “Plugins” → “Add New”. In the “Search Plugins” field, type “Advanced Custom Fields” and press return. Press the “Install Now” button, and then click on the “Activate Plugin” link on the screen that follows.

<img class="alignnone size-large wp-image-5637" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_07_PM-1024x819.png" alt="2_1_16__10_07_PM" width="632" height="505" />

### Step 4: Create a Custom Field Group

The core of Advanced Custom Fields is what it refers to as “Custom Field Groups”. These can be accessed by clicking on the “Custom Fields” menu item that appears on the admin sidebar.

Click on “Add New” (located next to the “Field Groups” header).

<img class="alignnone size-large wp-image-5638" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_13_PM-1024x819.png" alt="2_1_16__10_13_PM" width="632" height="505" />

In the Field Group’s title field, enter “Employee Information”.

### Step 5: Create Custom Fields

Press the “Add Field” button to create our first custom field. The first field we add will have the Field Label “Job Title”. Leave the Field Name to be the one that ACF assigns by default—in this case, “job_title”. Leave the Field Type as “Text” (the default), and leave all other default settings in place.

<img class="alignnone size-large wp-image-5640" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_18_PM-1024x1017.png" alt="2_1_16__10_18_PM" width="632" height="628" />

Click the “+ Add Field” button to create a new field. Call this field “Start Date”, leave the Field Name the default (“start_date”), and for the Field Type choose “Date Picker”. Leave all other field options at the default.

<img class="alignnone size-large wp-image-5641" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_19_PM-1024x1017.png" alt="2_1_16__10_19_PM" width="632" height="628" />

In the “Location” section, you need to tell WordPress under what conditions these fields should appear. The default, and the one you’ll be using, is to apply this field group to a particular post type. In this case, we want to display this field group when the Post Type is equal to “employee”.

<img class="alignnone size-large wp-image-5642" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_20_PM-1024x1017.png" alt="2_1_16__10_20_PM" width="632" height="628" />

Leave all other field group options as the default. Scroll up to the top of the page, and click on the “Publish” button in the left sidebar to activate this field group.

<img class="alignnone size-large wp-image-5643" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_21_PM-1024x1017.png" alt="2_1_16__10_21_PM" width="632" height="628" />

### Step 6: Create an “Employee” Post

Create a new post of the type “employee” by selecting “Employees → Add New” from the left sidebar in the administration. Put the employee’s name in the “Title” field, a brief biography in the content editor, and a photograph of the employee in the “Featured Image” field in the left sidebar.

Add the employee’s job title to the “Job Title” field that you created that appears below the content editor. Next. click on the “Start Date” field. A jQuery date picker will pop up. Use the date picker to select the employee’s start date.

<img class="alignnone size-large wp-image-5644" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_28_PM-1024x699.png" alt="2_1_16__10_28_PM" width="632" height="431" />

Click the “Publish” button.

### Step 7: Create a New Template to Display Employees

Copy the **single.php** template from the parent theme’s directory into the child theme’s directory, and rename it **single-employee.php**.

Create a directory in the child theme’s directory named **template-parts**. Copy the file **/template-parts/content-single.php** from the parent theme’s directory into the child theme’s **template-parts** directory. Do not rename the file.

In the **content-single.php** template part, add the following line beneath the line that outputs the post title (in this case, the employee’s name):
```PHP
<h2><?php echo esc_html( get_field( 'job_title' ) ); ?></h2>
```
Beneath the line that outputs the post’s content, add the following code:
```PHP
if ( '' !== get_field( 'start_date' ) ) {
  $date = DateTime::createFromFormat( 'Ymd', get_field( 'start_date' ) );
  echo 'Start date: ' . $date->format( 'F, Y' );
}
```
In the WordPress admin, in your new “Employee” post, click on the link to view the post. You’ll see the employee’s information complete with the employee’s name, photograph, the job title, and the start date (in full month, year format).

## Exercises

**Create a field that’s a <code>&lt;select&gt;</code> input.**

In the “Employee Information” field group, create a new field for which department the employee is in. Make it a “Select”-type field, populated with the following choices:
<pre>Account Services
Engineering
Creative</pre>
Edit the employee you created in the lesson to add which department that person is in, and edit the template to display this department after the employee’s job title.

**Assign a custom field group based on a different criterion.**

Create a new page template for your child theme. Create a new custom field group and assign it to all pages using the new page template.

## Quiz

**Which of the following is a benefit of Advanced Custom Fields?**

1.  Field validation
2.  Portability
3.  A variety of input types
4.  All of the above

**Answer:** 4. All of the above

**What function is used to display a custom field’s value in a template?**

1.  <code>display_field( $field_name );</code>
2.  <code>show_field( $field_name );</code>
3.  <code>the_field( $field_name );</code>
4.  <code>echo field( array( $fields[0] ) );</code>

**Answer:** 3. <code>the_field( $field_name );</code>

## Additional Resources
[ACF documentation](https://www.advancedcustomfields.com/resources/) page
