## README - components

<!-- START doctoc -->
<!-- END doctoc -->

### What belongs in the components folder?

The `components` folder is for holding code for smaller 
UI components and widgets that can be common to multiple
views. For example, a custom drop-down menu that can be
used by multiple views would belong in the `components`
folder.

### How is the components folder structured?

Each component should have its own subdirectory in the 
`components` folder. This should contain _all_ code
specific to that component, with the exception of Sass
code. This includes the tests for that component.

For example, the file structure for a component might
look like this:

    -views  
      |- dropdown   
          |- dropdown.component.ts    
          |- dropdown.component.test.ts
          |- dropdown.service.ts    
          |- dropdown.service.test.ts
          |- dropdown.html
