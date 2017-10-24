# recreate-lint-weirdness

This repository is a recreation of a weirdness I encountered with ember-cli-template-lint & the 'attribute-indentation' rule.

The following template is in application.hbs:

```hbs
{{thing-with-attributes-nonblock
  foo=5
  three=2
  six="seven"
}}
{{thing-with-attributes-nonblock
  foo=5
  three=2
  six="seven"
}}
{{thing-with-attributes-nonblock
  foo=5
  three=2
  six="seven"
}}
```
When running `npx ember-template-lint app/templates`, I get the following output:

```bash
/Users/katie/dev/recreate-lint-weirdness/app/templates/application.hbs
  7:2  error  Incorrect indentation of attribute 'foo' beginning at L7:C2. Expected 'foo' to be indentation at an of 7 but was found at 2  attribute-indentation
  8:2  error  Incorrect indentation of attribute 'three' beginning at L8:C2. Expected 'three' to be indentation at an of 7 but was found at 2  attribute-indentation
  9:2  error  Incorrect indentation of attribute 'six' beginning at L9:C2. Expected 'six' to be indentation at an of 7 but was found at 2  attribute-indentation
  12:2  error  Incorrect indentation of attribute 'foo' beginning at L12:C2. Expected 'foo' to be indentation at an of 12 but was found at 2  attribute-indentation
  13:2  error  Incorrect indentation of attribute 'three' beginning at L13:C2. Expected 'three' to be indentation at an of 12 but was found at 2  attribute-indentation
  14:2  error  Incorrect indentation of attribute 'six' beginning at L14:C2. Expected 'six' to be indentation at an of 12 but was found at 2  attribute-indentation

✖ 6 problems
```

To pass linting, I must change the template to:

```hbs
{{thing-with-attributes-nonblock
  foo=5
  three=2
  six="seven"
}}
{{thing-with-attributes-nonblock
       foo=5
       three=2
       six="seven"
}}
{{thing-with-attributes-nonblock
            foo=5
            three=2
            six="seven"
}}
```
