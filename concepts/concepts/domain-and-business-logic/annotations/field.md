# @io.skysail.domain.html.Field

The @Field annotation is one of the core elements of skysail. Look at this example:

```
@Getter
@Setter
@ToString
@GenerateResources(application = "myweight.TemplateApplication")
public class Weight implements Entity {

    @Id
    private String id;

    @Field
    private Date name;

}
```



