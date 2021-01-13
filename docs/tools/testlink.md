# TestLink export function

## Export case by suite

Modify file `testlink-root/apps/testlink/htdocs/gui/templates/testcases/containerViewTestSuiteTextButtons.inc.tpl`. Add code at line 33:

```html
<script>

    function export_by_suite(){
           const suite_id = document.getElementsByName('testsuiteID')[0].value;
           const suite_name = document.getElementsByName("testsuiteName")[0].value;
           const xhr = new XMLHttpRequest();
           xhr.open("POST", "http://localhost:5000/export/suite/", true);
           xhr.setRequestHeader('Content-Type', 'application/json');
           xhr.responseType = 'blob';
           xhr.onload = function(event){
                  const blob = xhr.response;
                  const a = document.createElement('a');
                  a.href = window.URL.createObjectURL(blob);
                  a.download = "Suite_" + suite_id + "_" + suite_name +".xlsx";
                  //a.dispatchEvent(new MouseEvent('click'));
                  a.click();
           };
           xhr.send(JSON.stringify({
                  "suite_id": suite_id,
                  "suite_name":suite_name
           }));
    }

</script>

<!-- Customized function: export test suite -->
<img class="clickable" src="{$tlImages.export_excel}" onclick="export_by_suite()" title="Export Test Suite" />
```

## Export case by plan

Modify file `testlink-root/apps/testlink/htdocs/gui/templates/execute/execDashboard.tpl`. Add code at line `64`:

```html
  <input type="hidden" id="plan_name" value="{$gui->testplan_name|escape}" />
  <img class="clickable" src="{$tlImages.export_excel}" onclick="export_by_plan()" title="Export Test Plan" />
  
  <script>
    function export_by_plan(){
      const plan_id = JSON.parse(restAPI.innerText).testPlanID;
      const plan_name = document.getElementById('plan_name').value;
      const xhr = new XMLHttpRequest();
      xhr.open("POST", "http://localhost:5000/export/plan/", true);
      xhr.setRequestHeader('Content-Type', 'application/json');
      xhr.responseType = 'blob';
      xhr.onload = function(event){
        if (xhr.readyState === xhr.DONE & xhr.status === 200){
            const blob = xhr.response;
            const a = document.createElement('a');
            a.href = window.URL.createObjectURL(blob);
            a.download = "Plan_" + plan_id + "_" + plan_name +".xlsx";
            // a.dispatchEvent(new MouseEvent('click'));
            a.click();
        }
        else{
          alert("No case found in plan: " + plan_name);
        }
      };
      xhr.send(JSON.stringify({
            "plan_id": plan_id,
            "plan_name":plan_name
      }));
    }
  </script>
```

## Hide unused menu items

### Hide project operation menu items

Modify file `testlink-root/apps/testlink/htdocs/gui/templates/testcases/containerView.tpl`

```html
<!-- comment off line 116 - 130 -->
<input type="image" src="{$tlImages.order_alpha}" name="reorder_testproject_testsuites_alpha"
       id="reorder_testproject_testsuites_alpha"
       onclick="doAction.value='reorder_testproject_testsuites_alpha'" title="{$labels.btn_reorder_testsuites_alpha}">

<img src="{$tlImages.import}" onclick="location='{$importToTProjectAction}'" title="{$labels.btn_import_testsuite}" />

{if $gui->canDoExport}
       <img src="{$tlImages.export}" onclick="location='{$tsuiteExportAction}'" title="{$labels.btn_export_all_testsuites}" />
{/if}

<img src="{$tlImages.report}" onclick="window.open('{$testSpecFullDocAction}')"
       title="{$labels.btn_gen_test_spec_new_window}" />

<img src="{$tlImages.report_word}" onclick="window.open('{$testSpecFullWordDocAction}')"
       title="{$labels.btn_gen_test_spec_word}" />
```

### Hide suite operation menu items

Modify file `testlink-root/apps/testlink/htdocs/gui/templates/testcases/containerViewTestSuiteTextButtons.inc.tpl`

```html
<!-- comment off line 77, 78 -->
<input type="image" src="{$tlImages.order_alpha}" name="reorder_testsuites_alpha" id="reorder_testsuites_alpha"
              onclick="doAction.value='reorder_testsuites_alpha'" title="{$labels.btn_reorder_testsuites_alpha}">

<!-- comment off line 83 - 90 -->
<img src="{$tlImages.report}" onclick="window.open('{$testSuiteDocAction}')"
       title="{$labels.btn_gen_test_suite_spec_new_window}" />

<img src="{$tlImages.report_word}" onclick="window.open('{$testSuiteWordDocAction}')"
       title="{$labels.btn_gen_test_suite_spec_word}" />

<img src="{$tlImages.import}" onclick="location='{$importToTSuiteAction}'" title="{$labels.btn_import_testsuite}" />
<img src="{$tlImages.export}" onclick="location='{$tsuiteExportAction}'" title="{$labels.btn_export_testsuite}" />

<!-- comment off line 133, 134 -->
<input type="image" src="{$tlImages.reorder}" name="reorder_testcases" id="reorder_testcases"
                 onclick="doAction.value='reorder_testcases'" title="{$gui->btn_reorder_testcases}">

<!-- comment off line 137 - 144 -->
<form method="post" action="{$basehref}lib/testcases/tcEdit.php">
       <input type="hidden" name="form_token" id="form_token" value="{$gui->form_token}" />
       <input type="hidden" name="doAction" id="doAction" value="" />
       <img src="{$tlImages.import}" onclick="location='{$importTestCasesAction}'" title="{$labels.btn_import_tc}" />
       <img src="{$tlImages.export}" onclick="location='{$exportTestCasesAction}'" title="{$labels.btn_export_tc}" />
       <img src="{$tlImages.create_from_xml}" onclick="location='{$createTCFromIssueMantisXMLAction}'"
              title="{$labels.btn_create_from_issue_xml}" />
</form>
```

### Hide case operation menu items

Modify file `testlink-root/apps/testlink/htdocs/gui/templates/testcases/tcView_viewer.tpl`

```html
<!-- comment off line 178 -->
<input type="submit" name="bulk_op" value="{$tcView_viewer_labels.btn_bulk}" />

<!-- comment off line 222, 223 -->
<input type="submit" name="do_create_new_version" title="{$tcView_viewer_labels.hint_new_version}"
       value="{$tcView_viewer_labels.btn_new_version}" />

<!-- comment off line 237, 238 -->
<input type="submit" name="{$act_deact_btn}"
       value="{lang_get s=$act_deact_value}" />

<!-- comment off line 254, 255 -->
<input type="submit" name="{$freeze_btn}"
    onclick="doAction.value='{$freeze_btn}';{$gui->submitCode}" value="{lang_get s=$freeze_value}" />

<!-- comment off line 260 -->
<input type="submit" name="delete_tc_version" value="{$tcView_viewer_labels.btn_del_this_version}" />

<!-- comment off line 274, 275 -->
<input type="button" id="addTc2Tplan_{$args_testcase.id}"  name="addTc2Tplan_{$args_testcase.id}"
       value="{$tcView_viewer_labels.btn_add_to_testplans}" onclick="location='{$hrefAddTc2Tplan}'" />

<!-- comment off line 284 -->
<input type="submit" name="export_tc" value="{$tcView_viewer_labels.btn_export}" />
```

## Change PHP timezone

Modify file `testlink-root/php/[etc]/php.ini`:

```ini
[Date]
; Defines the default timezone used by the date functions
; http://php.net/date.timezone
date.timezone = "Asia/Shanghai"
```

## Change font size in test specification tree view

Modify `testlink-root/apps/testlink/htdocs/third_party/ext-js/css/ext-all.css`

```css
/* change line 6250 to*/
.x-tree-node{
       color:#000;
       font: normal 12px arial, tahoma, helvetica, sans-serif;
}
```

## Create a custom config file

Create file `testlink-root/apps/testlink/htdocs/custom_config.inc.php` includes:

```php
<?php

# Set new user default language
$tlCfg->default_language = 'zh_CN';

# Disable user self sign up
$tlCfg->user_self_signup = FALSE;

/** User filter in Test Execution navigator - default value */
// logged_user -> combo will be set to logged user
// none        -> no filter applied by default
$tlCfg->exec_cfg->user_filter_default='logged_user';

# Display test suite operation panel by default
$tlCfg->gui->op_area_display->test_spec_container = 'inline'; // ''

# Display test case operation panel by default
$tlCfg->gui->op_area_display->test_case = 'inline'; // 'inline'
```

## Create a separate MySQL user

```sql
$ mysql -u root -p
> # enter password

mysql> CREATE USER 'export'@'%' IDENTIFIED BY '123456';
mysql> GRANT ALL PRIVILEGES ON bitnami_testlink.* TO 'export'@'%';
mysql> FLUSH PRIVILEGES;
mysql> quit
```

## Configure issue tracker

```xml
<!-- Template jirarestInterface -->
<issuetracker>
<username>JIRA USER NAME</username>
<password>PASSWORD</password>
<uribase>http://jira.yourcompany.com/</uribase>
<!-- CRITIC - WITH HTTP getIssue() DOES NOT WORK -->
<uriview>http://jira.yourcompany.com/browse/</uriview>
</issuetracker>
```