# Hook: deliveryLimitations
!> ***Documentation is incomplete***

## Getting Started
The deliveryLimitations hook allows plugins to add capabilities to Revive Adserver for defining delivery rules to be used as part of banner Delivery Options.

Revive Adserver supports 4 different groups within the deliveryLimitations hook:
- Client
- Geo
- Site
- Time

These `groups` relate, respectively, to the delivery rules provided by the:
- Client Delivery Rules;
- Geotargeting Delivery Rules;
- Site Delivery Rules; and
- Time Delivery Rules.
- Each delivery rule requires two files :



### Requirements
- **One file to define the way the way the rule is displayed in the UI, and how data for the rule is managed/stored:**
    - plugins/deliveryLimitations/`{$GROUP}`/`{$RULE}`.class.php
        - where `{$GROUP}` is one of the supported groups listed above; and
        - where `{$RULE}` is a string representing the delivery rule.
    - The file must define a class of the format:
        - ```php
        class Plugins_DeliveryLimitations_{$GROUP}_{$RULE} extends Plugins_DeliveryLimitations
        ```
    - The class may override methods from the parent `Plugins_DeliveryLimitations` class as required to define the details of how the delivery rule works.
- **One file to define the way the rule is processed during delivery of banners (i.e. if the rule matches or fails):**
    - plugins/deliveryLimitations/`{$GROUP}`/`{$RULE}`.delivery.php
    - The file must define a function of the format:
        - ```php
        function MAX_check{$GROUP}_{$RULE}($limitation, $op, $aParams = array())```
            - where `{$GROUP}` is one of the supported groups listed above; and
            - where `{$RULE}` is a string representing the delivery rule.
        - The function must return
            - **true**: if the rule passes (and the banner is permitted to be delivered); or
            - **false**: if the rule fails (and the banner is not permitted to be delivered)