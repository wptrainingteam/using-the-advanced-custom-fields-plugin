# Using The Advanced Custom Fields Plugin

<h2>Description</h2>
Advanced Custom Fields (ACF for short) is a plugin that allows you to create <i>custom field groups</i> for posts, pages, or custom post types. It provides a graphical user interface to add a variety of different field types including text fields, WYSIWYG areas, checkboxes, radio buttons, and more. In this lesson you'll learn how to set up the ACF plugin, how to create a custom field group for a custom post type, and how to display this information to a site visitor.
<h2>Prerequisite Skills</h2>
<ul>
 	<li><a href="https://make.wordpress.org/training/handbook/user-lessons/choosing-and-installing-plugins/">Ability to install a plugin</a></li>
 	<li>An understanding of <a href="https://make.wordpress.org/training/handbook/theme-school/custom-post-types/">post types</a> and <a href="https://codex.wordpress.org/Taxonomies">taxonomies</a></li>
 	<li>Ability to create <a href="https://make.wordpress.org/training/handbook/theme-school/child-themes/">a child theme</a> and <a href="https://make.wordpress.org/training/handbook/theme-school/custom-post-types/">a custom post type</a></li>
</ul>
<h2>Objectives</h2>
<ul>
 	<li>Students will be able to add custom fields to a custom post type and style the data stored in these fields in a custom theme template.</li>
</ul>
<h2>Assets</h2>
<ul>
 	<li><a href="https://wordpress.org/plugins/advanced-custom-fields/">Advanced Custom Fields plugin</a></li>
 	<li>Installation of WordPress</li>
 	<li><a href="https://wordpress.org/themes/twentysixteen/">The Twenty Sixteen theme</a></li>
</ul>
<h2>Screening Questions</h2>
<ul>
 	<li>Have you created content on a WordPress site?</li>
 	<li>Are you familiar with installing plugins?</li>
 	<li>Have you created a child theme?</li>
 	<li>Have you created a custom post type?</li>
 	<li>Are you comfortable editing theme templates?</li>
</ul>
<h2>Teacher Notes</h2>
<ul>
 	<li>Performing a live demonstration of identifying and installing the plugin from WordPress.org.</li>
 	<li>It is easiest for students to work on a locally installed copy of WordPress. Set some time aside before class to help students with installing WordPress locally if they need it. For more information on how to install WordPress locally, please visit our <a href="https://make.wordpress.org/training/teacher-resources/">Teacher Resources page</a>.</li>
 	<li>The preferred answer to the screening questions is “yes.” Participants who reply “no” to the screening questions may need more hands on guidance for this lesson, however they should be able to learn based on code samples etc.</li>
</ul>
<h2>Hands On Walkthrough</h2>
<h3>Introduction: What Is Advanced Custom Fields?</h3>
Welcome to Advanced Custom Fields! Today you are going to learn how to use this popular plugin - with over a million active installs - to extend WordPress' customizability.

Once you learn how to manipulate content on your WordPress site and create <a href="https://codex.wordpress.org/Post_Types">custom post types</a>, you’ll often want to extend the content storage capabilities of WordPress by creating custom fields. <a href="https://wordpress.org/plugins/advanced-custom-fields/">Advanced Custom Fields</a> provides a graphical user interface (GUI) for doing exactly that. This combination of custom post types and custom fields is what make WordPress a popular and full-featured content management system.

ACF offers the following benefits:
<ul>
 	<li><strong>Field validation</strong>: Certain types of fields, such as email, are validated to be sure they’re entered correctly.</li>
 	<li><strong>Flexibility:</strong> A wide selection of field types, including text fields, WYSIWYGs, file and image inputs, and several ways to reference other content on your WordPress site. Additionally, ACF provides some specialized field types that rely on jQuery: Google Maps, Date Picker, and Color Picker.</li>
 	<li><strong>Portability</strong>: Field groups can be exported and imported, and even converted into PHP code for inclusion into your custom theme or plugin, allowing them to be reused in different projects and managed in version control.</li>
</ul>
In this lesson, you will build a WordPress site for a mythical company, YayWP!. In addition to the default “page” and “post” post types, you’ll display the company’s employees on the site via a custom post type, complete with their job titles and start dates. Some of the native fields can be repurposed, but others will need to be created, and that’s where Advanced Custom Fields comes in.
<h3>Step 1: Create a Child Theme</h3>
Build a child theme from the Twenty Sixteen default theme. For now, create the <strong>style.css</strong> file and <strong>functions.php</strong> with the minimum needed to be recognized as a theme in the “Appearance” administration screen. If you need help, you can refer to the <a href="https://codex.wordpress.org/Child_Themes">Child Themes page in the WordPress Codex</a>.

Activate the child theme.
<h3>Step 2: Create a Custom Post Type for Employees</h3>
Using either a plugin like Custom Post Type UI or edit the <strong>functions.php </strong>file in your child theme, create the custom post type with the key “employee”. Here is the code to use in <strong>functions.php</strong>:
<pre>/**
 * Create a custom post type for employee information
 */

function employee_cpt() {
  $args = array(
    'labels'        =&gt; array(
      'name'          =&gt; _x( 'Employees', 'post type general name', 'twentysixteen-child' ),
      'singular_name' =&gt; _x( 'Employee', 'post type singular name', 'twentysixteen-child' )
    ),
    'description'   =&gt; __( 'Employee information.', 'twentysixteen-child' ),
    'public'        =&gt; true,
    'supports'      =&gt; array( 'title', 'editor', 'thumbnail' ),
    'menu_icon'     =&gt; 'dashicons-groups'
  );
  register_post_type( 'employee', $args );
}
add_action( 'init', 'employee_cpt' );</pre>
<img class="alignnone wp-image-5636 size-large" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_02_PM-1024x819.png" alt="2_1_16__10_02_PM" width="632" height="505" />

Via the Dashboard, navigate to “Settings” → “Permalinks” and choose a common permalink setting, then click “Save Changes”. <em>You <strong>must</strong> click “Save Changes”, even if you have not made any changes to your permalink settings, in order for WordPress to recognize posts with your new custom post type.</em>

<img class="alignnone size-large wp-image-5645" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_53_PM-1024x699.png" alt="2_1_16__10_53_PM" width="632" height="431" />
<h3>Step 3: Install the Advanced Custom Fields Plugin</h3>
Via the Dashboard, navigate to “Plugins” → “Add New”. In the “Search Plugins” field, type “Advanced Custom Fields” and press return. Press the “Install Now” button, and then click on the “Activate Plugin” link on the screen that follows.

<img class="alignnone size-large wp-image-5637" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_07_PM-1024x819.png" alt="2_1_16__10_07_PM" width="632" height="505" />
<h3>Step 4: Create a Custom Field Group</h3>
The core of Advanced Custom Fields is what it refers to as “Custom Field Groups”. These can be accessed by clicking on the “Custom Fields” menu item that appears on the admin sidebar.

Click on “Add New” (located next to the “Field Groups” header).

<img class="alignnone size-large wp-image-5638" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_13_PM-1024x819.png" alt="2_1_16__10_13_PM" width="632" height="505" />

In the Field Group’s title field, enter “Employee Information”.
<h3>Step 5: Create Custom Fields</h3>
Press the “Add Field” button to create our first custom field. The first field we add will have the Field Label “Job Title”. Leave the Field Name to be the one that ACF assigns by default—in this case, “job_title”. Leave the Field Type as “Text” (the default), and leave all other default settings in place.

<img class="alignnone size-large wp-image-5640" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_18_PM-1024x1017.png" alt="2_1_16__10_18_PM" width="632" height="628" />

Click the “+ Add Field” button to create a new field. Call this field “Start Date”, leave the Field Name the default (“start_date”), and for the Field Type choose “Date Picker”. Leave all other field options at the default.

<img class="alignnone size-large wp-image-5641" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_19_PM-1024x1017.png" alt="2_1_16__10_19_PM" width="632" height="628" />

In the “Location” section, you need to tell WordPress under what conditions these fields should appear. The default, and the one you’ll be using, is to apply this field group to a particular post type. In this case, we want to display this field group when the Post Type is equal to “employee”.

<img class="alignnone size-large wp-image-5642" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_20_PM-1024x1017.png" alt="2_1_16__10_20_PM" width="632" height="628" />

Leave all other field group options as the default. Scroll up to the top of the page, and click on the “Publish” button in the left sidebar to activate this field group.

<img class="alignnone size-large wp-image-5643" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_21_PM-1024x1017.png" alt="2_1_16__10_21_PM" width="632" height="628" />
<h3>Step 6: Create an “Employee” Post</h3>
Create a new post of the type “employee” by selecting “Employees → Add New” from the left sidebar in the administration. Put the employee’s name in the “Title” field, a brief biography in the content editor, and a photograph of the employee in the “Featured Image” field in the left sidebar.

Add the employee’s job title to the “Job Title” field that you created that appears below the content editor. Next. click on the “Start Date” field. A jQuery date picker will pop up. Use the date picker to select the employee’s start date.

<img class="alignnone size-large wp-image-5644" src="https://make.wordpress.org/training/files/2016/02/2_1_16__10_28_PM-1024x699.png" alt="2_1_16__10_28_PM" width="632" height="431" />

Click the “Publish” button.
<h3>Step 7: Create a New Template to Display Employees</h3>
Copy the <strong>single.php</strong> template from the parent theme’s directory into the child theme’s directory, and rename it <strong>single-employee.php</strong>.

Create a directory in the child theme’s directory named <strong>template-parts</strong>. Copy the file <strong>/template-parts/content-single.php</strong> from the parent theme’s directory into the child theme’s <strong>template-parts</strong> directory. Do not rename the file.

In the <strong>content-single.php</strong> template part, add the following line beneath the line that outputs the post title (in this case, the employee’s name):
<pre>&lt;h2&gt;&lt;?php echo esc_html( get_field( 'job_title' ) ); ?&gt;&lt;/h2&gt;</pre>
Beneath the line that outputs the post’s content, add the following code:
<pre>if ( '' !== get_field( 'start_date' ) ) {
  $date = DateTime::createFromFormat( 'Ymd', get_field( 'start_date' ) );
  echo 'Start date: ' . $date-&gt;format( 'F, Y' );
}</pre>
In the WordPress admin, in your new “Employee” post, click on the link to view the post. You’ll see the employee’s information complete with the employee’s name, photograph, the job title, and the start date (in full month, year format).
<h2>Exercises</h2>
<strong>Create a field that’s a <code>&lt;select&gt;</code> input.</strong>

In the “Employee Information” field group, create a new field for which department the employee is in. Make it a “Select”-type field, populated with the following choices:
<pre>Account Services
Engineering
Creative</pre>
Edit the employee you created in the lesson to add which department that person is in, and edit the template to display this department after the employee’s job title.

<strong>Assign a custom field group based on a different criterion.</strong>

Create a new page template for your child theme. Create a new custom field group and assign it to all pages using the new page template.
<h2>Quiz</h2>
<h3>Which of the following is a benefit of Advanced Custom Fields?</h3>
<ol>
 	<li>Field validation</li>
 	<li>Portability</li>
 	<li>A variety of input types</li>
 	<li>All of the above</li>
</ol>
<strong>Answer:</strong> 4. All of the above
<h3>What function is used to display a custom field’s value in a template?</h3>
<ol>
 	<li><code>display_field( $field_name );</code></li>
 	<li><code>show_field( $field_name );</code></li>
 	<li><code>the_field( $field_name );</code></li>
 	<li><code>echo field( array( $fields[0] ) );</code></li>
</ol>
<strong>Answer:</strong> 3. <code>the_field( $field_name );</code>
<h2>Additional Resources</h2>
<a href="https://www.advancedcustomfields.com/resources/">ACF documentation </a>page
