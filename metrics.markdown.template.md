<%- await include(`partials/activity.ejs`) %>

<% if (plugins.wakatime) { %> 
  **⏰ WakaTime <%= plugins.wakatime?.days ? `(over last ${{7:"week", 30:"month", 180:"6 months", 365:"year"}[plugins.wakatime.days]})` : "" %>**
  <% if (plugins.wakatime.error) { %>
    <%= plugins.wakatime.error.message %>
  <% } else { %>
    <% // left %>
    <% if (plugins.wakatime.sections.includes("time")) { %>
      ~<%= f(Math.ceil(plugins.wakatime.time.total)) %> coding hour<%= s(plugins.wakatime.time.total) %> recorded
    <% } %>
    <% if ((plugins.wakatime.sections.includes("projects"))&&(plugins.wakatime.projects?.length)) { %>
      Working on <%= f.ellipsis(plugins.wakatime.projects[0]?.name, {length:16}) %>
    <% } %>
    <% if ((plugins.wakatime.sections.includes("languages"))&&(plugins.wakatime.languages?.length)) { %>
      Mostly coding in <%= plugins.wakatime.languages[0]?.name %>
    <% } %>
    <% // right %>
    <% if (plugins.wakatime.sections.includes("time")) { %>
      ~<%= f(Math.ceil(plugins.wakatime.time.daily)) %> hour<%= s(plugins.wakatime.time.total) %> of coding per day
    <% } %>
    <% if ((plugins.wakatime.sections.includes("editors"))&&(plugins.wakatime.editors?.length)) { %>
      Coding with <%= plugins.wakatime.editors[0]?.name %>
    <% } %>
    <% if ((plugins.wakatime.sections.includes("os"))&&(plugins.wakatime.os?.length)) { %>
      Using <%= plugins.wakatime.os[0]?.name %>
    <% } %>
  <% } %> 
<% } %> 