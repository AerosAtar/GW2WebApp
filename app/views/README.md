##README - views

<!-- START doctoc -->
<!-- END doctoc -->

##What belongs in the views folder?
The `views` folder is for holding code specific to a
particular page of the application. For example, you
might have a view for the homepage, a view for the
login page, and a separate view for an admin page.

UI components and widgets that could be common to
several pages should _not_ be placed in the `views`
folder - they belong in the `components` folder.

##How is the views folder structured?
Each separate view for the application should have its
own subdirectory in the `views` folder. This should
contain _all_ code specific to that view, with the
exception of Sass code. This includes the tests for
that view.

For example, the file structure for a view might look
like this:

    - views   
        |- hero-panel
            |- hero-panel.controller.ts
            |- hero-panel.controller.test.ts
            |- hero-panel.service.ts
            |- hero-panel.service.test.ts
            |- hero-panel.html
