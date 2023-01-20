# Example models that combine the ECA and HTTP Client Manager Drupal modules

The examples were made on Drupal 10, ECA 1.1.0, and HTTP Client Manager 9.3.3.

For each example you need to:

1.  Install and enable the [ECA][1] module
    - Various ECA submodules are required, you can just enable all of them
2.  Install and enable the [BPMN.iO][2] module
3.  Install and enable the [HTTP Client Manager][3] module
4.  You can import each model by downloading the `tar.gz` file then going to
    `admin/config/workflow/eca/import` in your Drupal site

## Examples

- [Notify user of login][4]
- [Fill in SWAPI Person Data][5]

[1]: https://www.drupal.org/project/eca
[2]: https://www.drupal.org/project/bpmn_io
[3]: https://www.drupal.org/project/http_client_manager
[4]: notify-user-of-login.md
[5]: fill-in-swapi-person-data.md
