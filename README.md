# Plugin

# Type of Plugin
Authentication Scheme Type
Authorization Scheme Type
Dynamic Action
Item
Process
Region


# Item Type Plug-in Render Procedures must implement the following interface:

procedure <name of procedure> (
    p_item   in            apex_plugin.t_item,
    p_plugin in            apex_plugin.t_plugin,
    p_param  in            apex_plugin.t_item_render_param,
    p_result in out nocopy apex_plugin.t_item_render_result )
is
begin
  
  null;
  
end <name of procedure>;
