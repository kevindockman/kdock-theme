### **Theme Setup Prompt**

**Objective:** \> Initialize our custom HubSpot theme by generating the foundational `theme.json`, standard `style.css`, and the primary `base.html` template.

**Context Mapping:**

* Read `hubspot-theme-rules.md` to ensure strict adherence to HubSpot CMS boilerplate standards, required variables, and syntax.  
* Read `brand-guidelines.md` to establish our CSS variables (color palette, typography, etc.) within `theme.json` and `style.css`.

**Instructions:**

1. Generate a valid `theme.json` file incorporating our brand colors and fonts as theme settings.  
2. Generate a `style.css` file that references the HubSpot theme variables.  
3. Generate a `base.html` file. This must include the standard HubSpot header `{{ standard_header_includes }}`, footer `{{ standard_footer_includes }}`, a global header navigation section, a global footer section, and a central `{% block body %}{% endblock body %}` where child templates will inject their content.

**Output:** \> Provide the exact, complete code for `theme.json`, `style.css`, and `base.html`. Do not provide placeholder code; use the context provided to write production-ready code.
