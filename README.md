# Plugin

# Type of Plugin
<ul>
    <li>Authentication Scheme Type</li>
    <li>Authorization Scheme Type</li>
    <li>Dynamic Action</li>
    <li>Item</li>
    <li>Process</li>
    <li>Region</li>
</ul>

# Item Type Plug-in Render Procedures must implement the following interface:
<pre>
procedure name_of_procedure (
    p_item   in            apex_plugin.t_item,
    p_plugin in            apex_plugin.t_plugin,
    p_param  in            apex_plugin.t_item_render_param,
    p_result in out nocopy apex_plugin.t_item_render_result )
is
begin
  
  null;
  
end name_of_procedure;
</pre>
