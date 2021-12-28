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
  
  ---------------- Custom Attributes ----------------
  
--
  --Debug Mode
  --
  if apex_application.g_debug then
    apex_plugin_util.debug_page_item (
      p_plugin              => p_plugin,
      p_page_item           => p_item,
      p_value               => p_param.value,
      p_is_readonly         => p_param.is_readonly,
      p_is_printer_friendly => p_param.is_printer_friendly );
  end if;
  --
  --Printer Friendly Display
  --
  if p_param.is_printer_friendly then
    apex_plugin_util.print_display_only (
      p_item_name           => p_item.name,
      p_display_value       => p_param.value,
      p_show_line_breaks    => false,
      p_escape              => true,
      p_attributes          => p_item.element_attributes );

    p_result.is_navigable := false;
  --
  --Read Only Display
  --
  elsif p_param.is_readonly then
    apex_plugin_util.print_hidden_if_readonly (
      p_item_name           => p_item.name,
      p_value               => p_param.value,
      p_is_readonly         => p_param.is_readonly,
      p_is_printer_friendly => p_param.is_printer_friendly );

    p_result.is_navigable := false;
  else
    l_html := '<input type="text" id="' || p_item.name || '" name="' || p_item.name || '" ';
    l_html := l_html || '/>';

    sys.htp.p(l_html);

    --
    --Logging
    --
    if apex_application.g_debug then
      l_logging := true;
    else
      l_logging := false;
    end if;

    apex_javascript.add_onload_code (
      p_code => 'apexDateDropper.initDateDropper(' ||
                   apex_javascript.add_value (
                       p_value     => p_item.name,
                       p_add_comma => true )      || '{' ||
                                                       apex_javascript.add_attribute (
                                                           p_name      => 'format',
                                                           p_value     => l_format,
                                                           p_add_comma => true )       || '},' ||
                            || ');' );

    p_result.is_navigable := true;
  end if;
  
exception when others then raise;
  
end name_of_procedure;
</pre>
