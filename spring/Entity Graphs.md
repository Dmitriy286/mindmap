@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;

    //...
}

@Entity
public class Post {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String subject;
    @OneToMany(mappedBy = "post")
    private List<Comment> comments = new ArrayList<>();

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn
    private User user;
    
    //...
}

@Entity
public class Comment {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String reply;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn
    private Post post;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn
    private User user;
    
    //...
}

5. Defining an Entity Graph
To define an Entity Graph, we can either use the annotations on the entity or we can proceed programmatically using the JPA API.
5.1. Defining an Entity Graph with Annotations
The @NamedEntityGraph annotation allows specifying the attributes to include when we want to load the entity and the related associations.
So let’s first define an Entity Graph that loads the Post and his related entities User and Comments:

@NamedEntityGraph(
  name = "post-entity-graph",
  attributeNodes = {
    @NamedAttributeNode("subject"),
    @NamedAttributeNode("user"),
    @NamedAttributeNode("comments"),
  }
)

@Entity
public class Post {

    @OneToMany(mappedBy = "post")
    private List<Comment> comments = new ArrayList<>();
    
    //...
}

In this example, we’ve used the @NamedAttributeNode to define the related entities to be loaded when the root entity is loaded.
Let’s now define a more complicated Entity Graph where we want also load the Users related to the Comments.
For this purpose, we’ll use the @NamedAttributeNode subgraph attribute. This allows referencing a named subgraph defined through the @NamedSubgraph annotation:

@NamedEntityGraph(
  name = "post-entity-graph-with-comment-users",
  attributeNodes = {
    @NamedAttributeNode("subject"),
    @NamedAttributeNode("user"),
    @NamedAttributeNode(value = "comments", subgraph = "comments-subgraph"),
  },
  subgraphs = {
    @NamedSubgraph(
      name = "comments-subgraph",
      attributeNodes = {
        @NamedAttributeNode("user")
      }
    )
  }
)

@Entity
public class Post {

    @OneToMany(mappedBy = "post")
    private List<Comment> comments = new ArrayList<>();
    //...
}

The definition of the @NamedSubgraph annotation is similar to the @NamedEntityGraph and allows to specify attributes of the related association. Doing so, we can construct a complete graph.
In the example above, with the defined ‘post-entity-graph-with-comment-users’  graph, we can load the Post, the related User, the Comments and the Users related to the Comments.




Fetch Graph vs Load Graph

There are two types of EntityGraphs, Fetch and Load, which define if the entities not specified by attributeNodes of EntityGraphs should be fetched lazily or eagerly.

FETCH: It is the default graph type. When it is selected, the attributes that are specified by attribute nodes of the entity graph are treated as FetchType.EAGER and attributes that are not specified are treated as FetchType.LAZY.

LOAD: When this type is selected, the attributes that are specified by attribute nodes of the entity graph are treated as FetchType.EAGER and attributes that are not specified are treated according to their specified or default FetchType.



And we can assign the entity graph to repository methods as we like:

@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
    @EntityGraph(value =”graph-name”, type = EntityGraph.EntityGraphType.LOAD)
    List<Product> findAll();
}

links:

https://www.baeldung.com/spring-data-jpa-named-entity-graphs

