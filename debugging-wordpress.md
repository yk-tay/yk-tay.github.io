# Debugging Wordpress

## Outputting wordpress query variables

```echo var_export($GLOBALS['post'], TRUE);```

More verbose code, tells you the type of each variable (string, int, etc)

```global $wp_query;
var_dump($wp_query->query_vars);```

