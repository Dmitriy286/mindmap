# Using the FetchType.EAGER

   Not only the initialization of lazily fetched associations can cause lots of unexpected queries. That’s also the case if you use FetchType.EAGER. It forces Hibernate to initialize the association as soon as it loads the entity. So, it doesn’t even matter if you use the association or not. Hibernate will fetch it anyways. That makes it one of the most common performance pitfalls.
   And before you tell me that you never declare any eager fetching in your application, please check your to-one associations. Unfortunately, JPA defines eager fetching as the default behavior for these associations.
   OK, so how do you avoid these problems?
   Use FetchType.LAZY for all Associations
   You should use FetchType.LAZY for all of your associations. It’s the default for all to-many associations, so you don’t need to declare it for them explicitly. But you need to do that for all to-one association. You can specify the FetchType with the fetch attribute of the @OneToOne or @ManyToOne association.
   
   @Entity
   public class Review {

   @ManyToOne(fetch = FetchType.LAZY)
   @JoinColumn(name = "book_id")
   private Book book;

   ...
   }
