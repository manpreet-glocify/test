# Initial Release Plan DEVDOC

**Concept**: The funnelmap is a dynamic, interaction based routing mechanism for WordPress integrated into the AFP Core plugin features. It should allow the site owner to define branching paths that user will be redirected to depending on how they interact with the Funnelmap Block.

Generally this Block will provide an Accept / Decline type of offer for the visiting user to engage with, this is usually coupled with a financial capture transaction. Accepting the offer would execute billing of the user in real-time and then redirect them to a sub-offer page. Or the user could Decline the offer and get redirected to a separate offer page.

There should be no limit from a functional perspective of the system to how many branches a single Funnelmap can have. Each one should be associated to either:
1. An external page (which would break the user out of the Funnelmap)
1. An internal page (should return the post object, so we can use the post_id & permalink to redirect the user)

Visual Example: ![image](https://user-images.githubusercontent.com/5697218/199387346-108f2f34-629a-4aa5-af89-db9647acbba6.png)

***

## Requirements

- Custom Post Type
  > A custom post type is required to house the meta data for all the branches, pages and associations. This allows us to easily handle the meta data from a single post object (the CPT).
- Custom Meta Box
  > A custom meta box is required for the user interface that we want to use to make it easy for the user to Create, Edit and Manage their funnelmap. In addition to the meta information we can display back to the user about their funnelmap.
- WordPress Redirection
  > The funnel map controls the flow of the visiting user, it moves them from page to page while they are inside the funnel map, passing them through the different pages showing them the "offers"
- Gutenberg Block
  > To deliver the "OFFER" so a user can accept or decline, a Gutenberg block for WordPress needs to be created. Currently all the Blocks embedded into the AFP-Core plugin and its extensions are built using ACF, the same will be the case for this block.
- Elementor Block
  > AFP has an Elementor Extension where we replicate all the default Gutenberg blocks' functionality to an Elementor version.
- Payment Capture (Stripe & Authorize)
  > Currently AFP-Core has very basic payment capture mechanisms already attached. This needs to be expanded to include the new OFFER block feature of this funnelmap plugin.

***

## Dependencies

- AFP-Core
- ACF Pro

Currently the AFP-Core plugin (this will integrate with and rely on) has heavy integration with AdvancedCustomFields Pro, the ACF PRO plugin is embedded into AFP-Core. However, the ACF meta boxes don't fulfill some of the interface requirements we have. Because of this, we need our own custom metabox for user interaction and we'll save the data into ACF Meta fields. ACF PRO fields will handle the data and our custom metabox will manipulate that for the user (reading / writing to ACF meta).

This may seem counterintuitive, but it prevents us from needing to create our own settings savings, and we're already heavily using the ACF PRO framework. We can use the get_field mechanisms of ACF PRO and use their filter system to associate data in the back-end.

***

### Adobe XD Flow Examples

An empty metabox with no funnelmap data: https://xd.adobe.com/view/959f2d5a-4983-4364-aa21-22107e0f30b9-c0cc/

Detailed outline of a metabox with data: https://xd.adobe.com/view/62e146ee-246e-4ea7-99f7-51ff719dc105-37b2/

Further detail of managing a funnelmap metabox with data: https://xd.adobe.com/view/3d480969-73e6-48a7-8538-7f2d0657ff68-681b/
