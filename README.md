# Actions-yamler-secrets

**yamler** is a GitHub Action that processes an entire YAML document and makes all elements available to you as GitHub Workflow output variables, the output will be marked as sensitve value.

## Usage

```
- name: yamler
  uses: mildronize/actions-yamler-secrets@v1
  id: yamler
  with:
    yaml-file: "example.yaml"
    add-mark: true
```

## Output

yamler outputs the entire document as yamler-formatted output variable names. This serves as a good reference when the YAML document contains tags with characters not supported by GitHub Workflow variable names. yamler will automatically transform tags into friendly variable names.

In this example, the test file used is derived from [yaml.org](https://yaml.org). A deeper _number_ array was added to test for types other than string, object, and array.

```
***** Output Variables *****
yaml
what_it_is
yaml_resources__yaml_1_2_3rd_edition
yaml_resources__yaml_1_1_2nd_edition
yaml_resources__yaml_1_0_1st_edition
yaml_resources__yaml_issues_page
yaml_resources__yaml_mailing_list
yaml_resources__yaml_irc_channel
yaml_resources__yaml_cookbook_ruby
yaml_resources__yaml_reference_parser
projects__c_cpp_libraries__0
projects__c_cpp_libraries__1
projects__c_cpp_libraries__2
projects__ruby__0
projects__ruby__1
projects__ruby__2
projects__python__0
projects__python__1
projects__java__0
projects__java__1
projects__java__2
projects__java__3
projects__perl_modules__0
projects__perl_modules__1
projects__perl_modules__2
projects__perl_modules__3
projects__perl_modules__4
projects__cs__net__0
projects__cs__net__1
projects__php__0
projects__php__1
projects__php__2
projects__ocaml__0
projects__javascript__0
projects__javascript__1
projects__actionscript__0
projects__haskell__0
projects__others__0
related_projects__0
related_projects__1
related_projects__2
related_projects__3
related_projects__4
related_projects__5
number_object__number_sub_object__number_sub_sub_array__0
number_object__number_sub_object__number_sub_sub_array__1
number_object__number_sub_object__number_sub_sub_array__2
news__0
news__1
news__2
news__3
news__4
news__5
news__6
news__7
news__8
news__9
news__10
news__11
news__12
news__13
news__14
news__15
news__16
news__17
news__18
news__19
news__20
news__21
news__22
news__23
news__24
news__25
news__26
news__27
news__28
news__29
news__30
news__31
news__32
news__33
news__34
news__35
news__36
news__37
```

## Accessing Output Variables

yamler preserves document structure using double-underscore (\_\_) notation. If a value is located at `foo.bar`, the yamler output variable will become `foo__bar`. Arrays are indexed in a similar way, the element `bar.foo[5]`can be accessed with yamler at`bar__foo__5`.

```
# Use the output from the yamler step
- name: Output Test
run: |
  echo "${{ steps.yamler.outputs.yaml }}"
  echo "${{ steps.yamler.outputs.what_it_is }}"
  echo "${{ steps.yamler.outputs.yaml_resources__yaml_1_2_3rd_edition }}"
```
