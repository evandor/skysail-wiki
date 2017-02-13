# Annotations

Annotations are used to augment Entity and ValueObject definitions of your domain with additional information of how to format and render them.

An example of an "Account" Entity \(utilising lombok\) with various annotations:

```java
@Data
@EqualsAndHashCode(of = {"id"})
public class Account implements Entity {

    @Id
    private String id;

    /**
     * a (string-typed) attribute of this entity with a field annotation so that
     * it will be used in the entity rendering. There's a validation rule as well,
     * the field must not be blank.
     */
    @Field
    @NotBlank // not null or empty, trailing whitespaces getting ignored
    private String name;

    @Field
    @Pattern(regexp = "^$|^DE([0-9a-zA-Z]\\s?){20}$")
    private String iban;

    /**
     * This fields holds the creation date and is set in PostAccountResource when creating the new instance. It
     * should not be provided by the user in the creation form, so the visibility is set to 'hide'.
     */
    @Field(inputType = InputType.DATE)
    @PostView(visibility = Visibility.HIDE)
    @PutView(visibility = Visibility.HIDE)
    @JsonFormat (shape = JsonFormat.Shape.STRING, pattern = "dd-MM-yyyy hh:mm:ss")
    private Date created;

    @Field(inputType = InputType.READONLY)
    @ListView(hide = true)
    private String owner;

}
```



