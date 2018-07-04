## SHAREPOINT CUSTOMIZATIONS CAPABILITIES GUIDE

The following guide is meant to bring clarity to customizing SharePoint and help you choose technologies that you can safely rely on for the foreseeable future. The intent is to provide our best recommendations regarding current and upcoming customizing practices and to provide some additional insight in our recommendations.

> **Disclaimer:** This page is based on our experience in customizing SharePoint and we provide no guarantee to its completeness or accuracy.

Last Update: July 4, 2018

### Avoid

Customization capability|Status|Comments
------------------------|------|--------
Customization through DOM manipulation|Avoid|Not supported in the modern UI. Unreliable as the DOM in SharePoint Online is prone to frequent changes.
Custom Master Pages|Avoid|Not supported in the modern UI. Customization is not upgradeable and will likely need to be redone for the modern UI.
Custom Page Layouts|Avoid|Not supported in the modern UI. Customization is not upgradeable and will likely need to be redone for the modern UI.
Content/Script Editor Web Part-based solutions|Avoid|Hard to govern and manage centrally. Not available in modern UI. Use SharePoint Framework client-side web parts instead.
Customizing list forms|Avoid|Not supported in the modern UI. Blocks you from using the modern UI. Use client-side applications or Microsoft PowerApps instead
Adding web parts to list form pages|Avoid|Not supported in the modern UI. Blocks you from using the modern UI. Use client-side applications or Microsoft PowerApps instead.
Custom List Templates (Save List as Template)|Avoid|Impossible to manage. List instances tied to the original list and break when the original list is deleted. Consider using remote provisioning instead.
Custom List Definitions|Avoid|Rely on declarative provisioning. List instances tied to the list definition and break when the feature is removed. Consider using remote provisioning instead.
Custom Site Templates|Avoid|Rely on declarative provisioning that should be avoided. Consider using PnP provisioning engine and its templates instead.
Sandboxed Solutions with code|Avoid|Deprecated, not supported anymore.
SharePoint Designer Workflows|Avoid|Deprecated, use Microsoft Flow or 3rd party solutions instead.
InfoPath Forms|Avoid|Deprecated, use Microsoft PowerApps or 3rd party solutions instead.
SharePoint-hosted add-ins|Avoid|Limited functionality, consider using SharePoint Framework client-side web parts or provider-hosted add-ins if you need isolation or full-page applications.
Design Packages|Avoid|Rely on no-code Sandboxed Solutions, declarative provisioning and custom Master Pages all of which should be avoided.
Access applications|Avoid|Deprecated. Consider using Microsoft PowerApps instead.
Declarative provisioning via no-code Sandboxed Solutions|Avoid|Based on declarative provisioning which should be avoided due to its limitations. Use remote provisioning instead.
JavaScript Object Model|Avoid|Limited and not invested in anymore. Consider using REST or SP PnP JS Core instead
Event Receivers and List Event Receivers|Avoid|Event Receivers and List Event Receivers can only be used in on-premises environments as they require to be created with full trust code. Consider using Remote Event Receivers or Webhooks instead.
Timer Jobs|Avoid|Timer Jobs can only be used in on-premises environments as they require full trust code. Consider developing your timer based jobs as Azure Web Jobs or Azure Functions.

### Caution

Customization capability|Status|Comments
------------------------|------|--------
Ribbon customization via User Custom Actions|Caution|Support for user custom actions is limited in the modern UI. If you have ribbon actions using a simple URL with URL token, they will work on classic and modern UI's. If you use anything else, then avoid this and use SharePoint Framework Extensions instead. See https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-customizations-customize-lists-and-libraries#user-custom-actions for the supported scenarios.
JS Link|Caution|While not upgradeable to the modern UI, JS Link is the only way to customize fields for the classic UI. For full support of both the classic and the modern UI needs to be complimented by SharePoint Framework extensions.
Script injection via User Custom Actions|Caution|Required to customize the classic UI. Avoid DOM manipulation as its error-prone and not supported in the modern UI.
Display Templates|Caution|Necessary to customize the classic SharePoint Search results but not upgradeable to the modern UI. Will likely need to be redone from scratch for the modern UI.
Content Query Web Part-based solutions|Caution|Limited to a single site collection but often required when you can't wait for new content to be crawled by search. If search latency is not an issue, consider using Content Search Web Part instead which is more powerful.
Content Search Web Part-based solutions|Caution|Not available in the modern UI. Customization will likely need to be redone from scratch for the modern UI.
Search Query Web Part-based solutions|Caution|Not available in the modern UI. Customization will likely need to be redone from scratch for the modern UI.
Content Type Hub|Caution|Often required for ECM scenarios but beware of timing issues when creating new sites. Content Types are also not added to new document libraries. Consider using remote provisioning instead.
Classic team sites|Caution|No new features are being added to at the moment. Consider using modern team sites instead.
Publishing Sites|Caution|The only way to implement publishing in SharePoint, but at the moment has unclear future regarding how publishing will look like on top of the SharePoint Framework and to what extent current customization efforts will be upgradeable. The new Communication sites is an option, but does not currently have feature parity on for example multi language support, content approval, set publish dates and custom page layouts - so depending on your need, they might not be a perfect match right now. It is, however, possible to use code to program in these features, but might not give a great ROI in the long run.
Remote Event Receivers|Caution|Remote Event Receivers allow you to interact with events of lists that are go**ing** to happen or happen**ed**. Be careful when using Remote Event Receivers as it does not have a retry-mechanism. If you only require interacting with your application when events happened, then please consider to check out SharePoint Webhooks.
AadHttpClient|Caution|Powerful capability to connect SharePoint Framework solutions to APIs secured with Azure AD. Currently in preview. Research, but don't use in production just yet. For more information see https://docs.microsoft.com/en-us/sharepoint/dev/spfx/use-aadhttpclient
MSGraphClient|Caution|Powerful capability to connect SharePoint Framework solutions to the Microsoft Graph. Currently in preview. Research, but don't use in production just yet. For more information see https://docs.microsoft.com/en-us/sharepoint/dev/spfx/use-msgraph
Microsoft PowerApps|Caution|Actively developed and invested in. PowerApps must be republished at least once every 6 months or they might stop working. For more information see https://docs.microsoft.com/en-us/powerapps/maker/canvas-apps/save-publish-app

### Do

Customization capability|Status|Comments
------------------------|------|--------
Custom Content Types|Do|Required for ECM scenarios. Avoid declarative provisioning and use remote provisioning instead.
Custom Site Columns|Do|Required for ECM scenarios. Avoid declarative provisioning and use remote provisioning instead.
Single Page Applications hosted in SharePoint|Do|Still a reliable way of building applications for SharePoint Online. No alternative in the SharePoint Framework available at the moment.
Provider-hosted add-ins|Do|Still valid approach for building SharePoint solutions. Consider SharePoint Framework client-side web parts instead unless you require web part isolation.
SharePoint Framework client-side web parts|Do|Supported in both classic and modern UI. Actively developed and invested in.
SharePoint Framework extensions|Do|Supported in modern UI. Actively developed and invested in. When working with classic UI, you need to use their equivalents such as Custom Actions or JSLink.
Client-Side Object Model (CSOM)|Do|Simplifies communicating with SharePoint, actively managed. SLA-backed by Microsoft.
SP PnP JS Core|Do|Significantly simplifies communicating with SharePoint in client-side solutions. Keep in mind that it's a community-driven effort with no SLA behind it.
SP PnP Core|Do|Significantly simplifies communicating with SharePoint. Keep in mind that it's a community-driven effort with no SLA behind it.
Microsoft Flow|Do|Actively developed and invested in. Take into consideration that all flows are linked to users who created them. Also take a look at Logic Apps, which is the technology behind Flow. See https://docs.microsoft.com/en-us/azure/azure-functions/functions-compare-logic-apps-ms-flow-webjobs for information on when to use Flow and when to use Logic Apps.
Microsoft Logic Apps|Do|Actively developed and invested in. See https://docs.microsoft.com/en-us/azure/azure-functions/functions-compare-logic-apps-ms-flow-webjobs for information on when to use Flow and when to use Logic Apps.
SharePoint Webhooks|Do|SharePoint Webhooks is a relative new functionality which allows you to receive notification when events happen**ed** in your lists. When an event happened, SharePoint sends minimal information about it to your service. If someone might intercept such a message, the data is irrelevant as it only contains IDs. Your service has to actually gather the changes. Another key feature of SharePoint webhooks is that it has a retry-mechanism. Be aware that webhooks can only be used for events that happened. This does not cover events currently **happening**.
Long-running operations (SharePoint Online)|Do|When you want to develop long-running operations for SharePoint Online you have two options: Azure Functions or Web Jobs. Both can achieve the same thing, although the user experience of Azure Functions is better. Be aware that when running Functions on a consumption plan, the tasks have a 5-minute timeout. This timeout is removed when your Azure Function app is configured with an App Service plan.
Long-running operations (on-premises)|Do|When you want to develop long-running operations for SharePoint on-premises you can do this with scheduled tasks. Here you can choose for PowerShell (optional in combination with SP PnP PowerShell) or a console app.
Modern team sites|Do|Actively developed and invested in. Regularly extended with new features. Group different workloads like conversations, documents and tasks to better facilitate collaboration. Also, offer native support for mobile devices.
Communication sites|Do|Actively developed and invested in. Regularly extended with new features. While not a full-featured replacement for classic publishing sites just yet, they become more powerful as more capabilities are being added. Also, offer native support for mobile devices.
Hub sites|Do|Powerful capability to organize sites in your portal.