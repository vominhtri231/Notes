# Spring validation intro

## Precondition

To use spring validation, you must include the dependency: `spring-boot-starter-validation`
(or any dependency that include it, eg `spring-boot-starter-web`)

## Validation annotation

Spring validation support JSR-303 Bean validation (which is a Java validate api for Java EE and Java SE), but this can be toggled on/off. It came validation annotations, the most common are:

* @NotNull
* @NotEmpty
* @NotBlank
* @Min and @Max
* @Pattern
* @Email

```java
class Student{
    @NotBlank
    private String name;

    ...
}
```

## Validator

Validator is the interface responsible for checking the constraints. Spring provide us the pre-configured Validator which can be injected.

```java
Set<ConstraintViolation<Student>> violations = validator.validate(student);
```

## Applying validation

To apply validation, using:

* `@Valid`  
This is from JSR-303, which is used for method level and member attribute validation. The fail validation would throw `MethodArgumentNotValidException`.

```java
  ResponseEntity<String> createStudent(@Valid @RequestBody Student student) {
    return ResponseEntity.ok("valid");
  }
```

  If the type contains a field with complex type that need to be validate, it should be annotated with `@Valid`, too.

* `@Validated`  
A Spring variant of @Valid and support validation group. It can also be applied to class - which will validate parameters are passed to methods of the class. The fail validation would throw `ConstraintViolationException` instead.

```java
@Validated
class Student {
  public void setName(@NotBlank name) {

  }
}
```
