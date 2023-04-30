# Entity graph

To provide which fields to load dynamically instead of the defautl fetch plain in entity, we could use entity graph.

## Declaration 

To declared a entity graph, we could use `NamedEntityGraph` annotation, using `subgraphs` for declare nested graphes.

```java
@Entity
@NamedEntityGraph(name = "GroupInfo.withMember",
  attributeNodes = @NamedAttributeNode("members"))
@NamedEntityGraph(name = "GroupInfo.withMemberDetail",
  attributeNotes = {@NamedAttributeNode("members"), @NamedAttributeNode("children")},
  subgraphs = {
    @NamedSubgraph(
      name = "member-subgraph",
      attributeNodes = {
        @NamedAttributeNode("sub")
      }
    )
  })
public class GroupInfo {
  @ManyToMany
  List<GroupMember> members = new ArrayList<GroupMember>();

  …
}
```

Or we can create entity graph programatically.

```java
EntityGraph<Post> entityGraph  = entityManager.createEntityGraph(GroupInfo.class);
entityGraph.addAttributeNodes("members");
```

## Usage

JPA uses entity graph as a hint 
```java
entityManager
  .createQuery("...")
  .setHint("javax.persistence.fetchgraph", entityGraph)
```

## Category

There are too type of entity graph:

- FETCH: All attributes in the graph are treated as EAGER, others are treated as LAZY. The hint `javax.persistence.fetchgraph` would be used
- LOAD: All attributes in the graph are treated as EAGER, other are treated as their specified type or default. The hint `javax.persistence.loadgraph` would be used
