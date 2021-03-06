# Fields

## Field Types

Field types are plugins in Drupal 8.

* [Field type plugins in Drupal 8](http://cgit.drupalcode.org/drupal/tree/core/lib/Drupal/Core/Field/Plugin/Field/FieldType)

Standard field types are below. The ID should be used when defining a field as part of an entity schema, for example.

| Class                 | ID               | Notes                                      |
| --------------------- | ---------------- | ------------------------------------------ |
|   BooleanItem         | boolean          |                                            |
|   ChangedItem         | changed          | UNIX timestamp                             |
|   CreatedItem         | created          | UNIX timestamp                             |
|   DecimalItem         | decimal          |                                            |
|   EmailItem           | email            |                                            |
|   EntityReferenceItem | entity_reference |                                            |
|   FloatItem           | float            |                                            |
|   IntegerItem         | integer          |                                            |
|   LanguageItem        | language         |                                            |
|    MapItem            | map              | Serialized array of values                 |
|   PasswordItem        | password         |                                            |
|   StringItem          | string           |                                            |
|   StringLongItem      | string_long      | Creates either a blob or text field in MySQL. [Example](http://cgit.drupalcode.org/drupal/tree/core/lib/Drupal/Core/Field/Plugin/Field/FieldType/StringLongItem.php#n31). |
|   TimestampItem       | timestamp        |                                            |
|   UriItem             | uri              |                                            |
|   UuidItem            | uuid             |                                            |

## Field Info

`field_info_fields()` is deprecated in Drupal 8. Use [\Drupal::entityManager()->getFieldMap()](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Entity!EntityManager.php/function/EntityManager%3A%3AgetFieldMap/8)

## Creating a Custom Field Type

See [MailChimp Lists module for an example of a custom field type](https://github.com/thinkshout/mailchimp/tree/8.x-1.x/modules/mailchimp_lists/src/Plugin/Field).

* [MailchimpListsSubscription field](https://github.com/thinkshout/mailchimp/blob/8.x-1.x/modules/mailchimp_lists/src/Plugin/Field/FieldType/MailchimpListsSubscription.php)

### Compared to Drupal 7

| Drupal 7                                | Drupal 8 |
| --------------------------------------- | -------- |
| hook_field_settings_form()              | [FieldItemInterface::storageSettingsForm](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Field%21FieldItemInterface.php/function/FieldItemInterface%3A%3AstorageSettingsForm/8) |
| hook_field_instance_settings_form()     | [FieldItemInterface::fieldSettingsForm](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Field%21FieldItemInterface.php/function/FieldItemInterface%3A%3AfieldSettingsForm/8) |
| hook_field_presave()                    | [FieldItemInterface::preSave](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Field%21FieldItemInterface.php/function/FieldItemInterface%3A%3ApreSave/8) |
| hook_field_formatter_settings_form()    | [FormatterInterface::settingsForm](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Field!FormatterInterface.php/function/FormatterInterface%3A%3AsettingsForm/8) |
| hook_field_formatter_settings_summary() | [FormatterInterface::settingsSummary](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Field!FormatterInterface.php/function/FormatterInterface%3A%3AsettingsSummary/8) |
| hook_field_formatter_view()             | [FormatterInterface::view](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Field!FormatterInterface.php/function/FormatterInterface%3A%3Aview/8) |
| hook_field_prepare_view()               | [FormatterInterface::prepareView](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Field!FormatterInterface.php/function/FormatterInterface%3A%3AprepareView/8) |

**Important**

* `FieldItemInterface::storageSettingsForm` will *not work* unless you implement [FieldItemInterface::defaultStorageSettings](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Field!FieldItemInterface.php/function/FieldItemInterface%3A%3AdefaultStorageSettings/8)
* `FieldItemInterface::fieldSettingsForm` will *not work* unless you implement [FieldItemInterface::defaultFieldSettings](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Field!FieldItemInterface.php/function/FieldItemInterface%3A%3AdefaultFieldSettings/8)

#### Database Structure

Drupal 7 `field_config` table

* Field configuration now stored in `config` table
* ID structure is field . storage . `$entity` . field _ `$field_name`

Drupal 7 `field_config_instance` table

* Field instance configuration now stored in `config` table
* ID structure is field . field . `$entity` . field _ `$field_name`
