# Entity graph

For those lazy init fields, to provide a hint for JPA to load those fields, we could use entity graph.

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

## Usage

To use the entity graph:

```java
@Repository
public interface GroupRepository extends CrudRepository<GroupInfo, String> {

  @EntityGraph(value = "GroupInfo.withMember", type = EntityGraphType.LOAD)
  GroupInfo getByGroupName(String name);

}
```

Under the hood, JPA would pass the entity graph as a hint 
```java
query.setHint("javax.persistence.fetchgraph", entityGraph)
```

## Category

There are too type of entity graph:

- FETCH: All attributes in the graph are treated as EAGER, others are treated as LAZY. The hint `javax.persistence.fetchgraph` would be used
- LOAD: All attributes in the graph are treated as EAGER, other are treated as their specified type or default. The hint `javax.persistence.loadgraph` would be used
