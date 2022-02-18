# Bean discovery

When application is started, CDI container will perform bean discovery - search for all bean the classpath.

By default, only Bean that annotated with Scope, Interceptor, Decorator and Stereotype will be discovered

You could change this policy with property `bean-discovery-mode` in `beans.xml`.
