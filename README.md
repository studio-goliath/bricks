<h1>Bricks</h1>

Bricks plugin provide the main functions to display brick templates provided by any other thematic bricks plugins (bricks-basic-templates, bricks-image-templates)
Therefore this plugin does not do anything without at least one thematic bricks plugin activated.

A thematic bricks plugin provides a bundle of brick templates.

<h2>How to create a new brick (related to its thematic)</h2>

A brick should contain :

* A template part located in bricks-{{ thematic_name }}-templates/parts/row-{{ brick_name }}.php
* Css files located in bricks-{{ thematic_name }}-templates/css
* Js files (if needed) located in bricks-{{ thematic_name }}-templates/js
* ACF declarations (fields)

Css files :

Css files have to be registered in bricks_basic_add_styles function located in bricks-{{ thematic_name }}-templates/bricks-{{ thematic_name }}-templates.php

<pre><code>
return array_merge($scripts,
    array(
        'full-width-image' => array(
            'brick-full-width-image' => $plugin_dir_url . '/css/full-width-image.min.css'
        ),
        'slider' => array(),
        'parallax' => array()
    )
);
</code></pre>

Js files :

Js files have to be registered in bricks_image_add_scripts function located in bricks-{{ thematic_name }}-templates/bricks-{{ thematic_name }}-templates.php

<pre><code>
return array_merge($scripts,
    array(
        'slider' => array(
            'brick-slick' =>  $plugin_dir_url . '/js/slick.min.js',
            'brick-slider' =>  $plugin_dir_url . '/js/slider.min.js',
        ),
        'parallax' => array()
    )
);
</code></pre>

ACF declarations :

ACF declarations have to be registered in bricks_image_add_templates function located in bricks-{{ thematic_name }}-templates/bricks-{{ thematic_name }}-templates.php

<pre><code>
return array_merge($layouts,
        array(
            array(
                'key' => '575e642a75784',
                'name' => 'full-width-image',
                'label' => 'Full width image',
                'display' => 'row',
                'sub_fields' => array(
                    array(
                        'key' => 'field_575e643a75785',
                        'label' => 'Image',
                        'name' => 'image',
                        'type' => 'image',
                        'instructions' => '',
                        'required' => '',
                        'conditional_logic' => '',
                        'wrapper' => array(
                            'width' => '',
                            'class' => '',
                            'id' => '',
                        ),
                        'return_format' => 'array',
                        'preview_size' => 'thumbnail',
                        'library' => 'all',
                        'min_width' => '',
                        'min_height' => '',
                        'min_size' => '',
                        'max_width' => '',
                        'max_height' => '',
                        'max_size' => '',
                        'mime_types' => '',
                    ),
                ),
                'min' => '',
                'max' => '',
            ),
            array(
                // ACF declarations
            )
        )
    );
</code></pre>

<h2>Add the brick to brick_template filter</h2>

bricks_display_image_template function will take care of displaying the template in pages, posts or custom post type.
Therefore it is a must to add a filter for every brick with the bricks_display_image_template function.

<code>add_filter( 'brick_template_{{ brick_name }}', 'bricks_display_image_template' , 10, 2 );</code>


You should be good to go at that point! Cheers!