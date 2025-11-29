---
title: HTTP flows with Requests and Responses for Adobe Campaign
categories: [http,opensource,adobe campaign]
---
Excerpt here...
<p class="text-center">🐍👑🌍</p>
<!--more-->
**bold** *italic*  ~~strikethrough~~

## Intro

- Logon sequence

## Get config

- `GET /r/config`

- Response

```xml
404
```

## Logon

- `POST /nl/jsp/soaprouter.jsp` with `SOAPAction: xtk:session#Logon`

```xml
<?xml version='1.0'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
    xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:xtk:session'
    xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
        <Logon xmlns='urn:xtk:session'
            SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
            <__sessiontoken xsi:type='xsd:string'></__sessiontoken>
            <strLogin xsi:type='xsd:string'>admin</strLogin>
            <strPassword xsi:type='xsd:string'>admin</strPassword>
            <elemParameters xsi:type='ns:Element'
                SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
                <client build="9364" />
            </elemParameters>
        </Logon>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

- Response

```xml
<?xml version='1.0'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
    xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:xtk:session'
    xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
        <LogonResponse xmlns='urn:xtk:session'
            SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
            <pstrSessionToken xsi:type='xsd:string'>___7bb151d2-ee05-4bd2-9d5e-23e83547c528</pstrSessionToken>
            <pSessionInfo xsi:type='ns:Element'
                SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
                <sessionInfo>
                    <serverInfo advisedClientBuildNumber="0" advisedClientName=""
                        advisedClientVersion="" allowSQL="false" buildNumber="9364"
                        commitId="8f3ef8e" databaseId="uFE80000000000000DB5D321FB1AEA122749CE455"
                        defaultNameSpace="cus" fohVersion="2" instanceName="instance1" majNumber="6"
                        minClientBuildNumber="9333" minNumber="7" minNumberTechnical="0"
                        releaseName="7.3.4" securityTimeOut="86400"
                        serverDate="2025-11-29 22:33:07.413Z" servicePack="0" sessionTimeOut="86400"
                        useVault="false" webView2Mode="1" />
                    <userInfo datakitInDatabase="true" homeDir="" instanceLocale="en-US"
                        locale="en-US" login="admin" loginCS="Administrator (admin)" loginId="1059"
                        noConsoleCnx="false" orgUnitId="4570" theme="" timezone="America/New_York">
                        <login-group id="1060" />
                        <login-right right="admin" />
                        <installed-package name="billing" namespace="nms" />
                        <installed-package name="campaign" namespace="nms" />
                        <installed-package name="core" namespace="nms" />
                        <installed-package name="coreInteraction" namespace="nms" />
                        <installed-package name="country" namespace="nms" />
                        <installed-package name="coupon" namespace="nms" />
                        <installed-package name="folder" namespace="nms" />
                        <installed-package name="gdpr" namespace="nms" />
                        <installed-package name="heatmap" namespace="nms" />
                        <installed-package name="japanLoc" namespace="nms" />
                        <installed-package name="messageCenter" namespace="nms" />
                        <installed-package name="messageCenterControl" namespace="nms" />
                        <installed-package name="messageCenterExec" namespace="nms" />
                        <installed-package name="report" namespace="nms" />
                        <installed-package name="ruleset" namespace="nms" />
                        <installed-package name="systemStrings" namespace="nms" />
                        <installed-package name="acc_web" namespace="unofficialacc" />
                        <installed-package name="commonlibraries" namespace="unofficialacc" />
                        <installed-package name="views" namespace="unofficialacc" />
                        <installed-package name="core" namespace="xtk" />
                    </userInfo>
                    <option name="NmsTracking_UrlDelimiters" type="6" value="() {} []" />
                    <option name="Nms_DefaultRcpSchema" type="6" value="nms:recipient" />
                </sessionInfo>
            </pSessionInfo>
            <pstrSecurityToken xsi:type='xsd:string'>
                @DrRFO29Bk9-[...]oqyGLTsWjxC9Q==</pstrSecurityToken>
        </LogonResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## GetDirtyCacheEntities

- POST `/nl/jsp/soaprouter.jsp` with `SOAPAction: xtk:persist#GetDirtyCacheEntities`

```xml
<?xml version='1.0'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
    xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:xtk:persist'
    xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
        <GetDirtyCacheEntities xmlns='urn:xtk:persist'
            SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
            <__sessiontoken xsi:type='xsd:string'></__sessiontoken>
            <domCacheEntities xsi:type='ns:Element'
                SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
                <cache>
                    <xtk:schema>
                    <entityCache md5="610172FF368985BB400637C70EDBD29B" pk="xtk:xslt" />
                    <entityCache md5="42862CBA941BCA9A6BB02452A6156ED5" pk="xtk:workflowTask" />
                    <entityCache md5="AA9DE0E06006AF1496386832C27067BC" pk="xtk:workflowLog" />
                    <entityCache md5="38BEE244B12994F67A6B41F50878E397" pk="xtk:workflowJob" />
                    [...]
                    <entityCache md5="392E16D4DD441BDBC2620971443B61E7" pk="nms:deliveryDet" />
                    <entityCache md5="F8D58D81ABB3845169A65A08D74C91C8"
                        pk="nms:deliveryCustomization" />
                    <entityCache md5="D98E07FC03616990B16890D042C88229" pk="nms:delivery" />
                    </xtk:form>
                </cache>
            </domCacheEntities>
        </GetDirtyCacheEntities>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

- Response

```xml
<?xml version='1.0'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
    xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:wpp:default'
    xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
        <GetDirtyCacheEntitiesResponse xmlns='urn:wpp:default'
            SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
            <pdomDirtyEntities xsi:type='ns:Element'
                SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
                <cache />
            </pdomDirtyEntities>
        </GetDirtyCacheEntitiesResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## Get timezone

- `GET /xtk/jsp/zoneinfo.jsp?name=America%2FNew_York`

- Response

```xml
TZif2
```

## UseScrollBar

- POST xx with `SOAPAction: xtk:session#GetOption`

```xml
<?xml version='1.0'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
    xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:xtk:session'
    xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
        <GetOption xmlns='urn:xtk:session'
            SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
            <__sessiontoken xsi:type='xsd:string'></__sessiontoken>
            <strName xsi:type='xsd:string'>XtkUseScrollBar</strName>
        </GetOption>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

- Response

```xml
<?xml version='1.0'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
    xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:xtk:session'
    xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
        <GetOptionResponse xmlns='urn:xtk:session'
            SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
            <pstrValue xsi:type='xsd:string'></pstrValue>
            <pbtType xsi:type='xsd:byte'>0</pbtType>
        </GetOptionResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## Get FFDA

- POST  with `SOAPAction: xtk:folder#LoadChildrenWithPath`

```xml
<?xml version='1.0'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
    xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:xtk:session'
    xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
        <GetOption xmlns='urn:xtk:session'
            SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
            <__sessiontoken xsi:type='xsd:string'></__sessiontoken>
            <strName xsi:type='xsd:string'>NmsServer_FFDA_Datasource</strName>
        </GetOption>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

- Response
```xml
<?xml version='1.0'?><SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:xtk:session' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'><SOAP-ENV:Body><GetOptionResponse xmlns='urn:xtk:session' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'><pstrValue xsi:type='xsd:string'></pstrValue><pbtType xsi:type='xsd:byte'>0</pbtType></GetOptionResponse></SOAP-ENV:Body></SOAP-ENV:Envelope>
```

## Get x

- POST xx with `SOAPAction: xtk:queryDef#ExecuteQuery`

```xml
<?xml version='1.0'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
    xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:xtk:queryDef'
    xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
        <ExecuteQuery xmlns='urn:xtk:queryDef'
            SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
            <__sessiontoken xsi:type='xsd:string'></__sessiontoken>
            <entity xsi:type='ns:Element'
                SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
                <queryDef operation="select" schema="xtk:queryFilter" startPath="/"
                    xtkschema="xtk:queryDef">
                    <select>
                        <node expr="@id" />
                        <node expr="@name" />
                        <node expr="@label" />
                        <node expr="@hasForm" />
                        <node expr="@default" />
                        <node expr="@startPath" />
                        <node expr="@sqlTable" />
                        <node expr="[where/@displayFilter]" />
                        <node expr="[where/@extendedSchema]" />
                        <node expr="[where/@forceHint]" />
                        <node expr="[where/@filterName]" />
                        <node anyType="true" expr="[where/condition]" noComputeString="true" />
                        <node anyType="true" expr="[where/ctx]" />
                        <node expr="[where/@filteringSchema]" />
                        <node anyType="true" expr="form" />
                        <node expr="@img" />
                        <node expr="@shortCut" />
                        <node expr="@main" />
                        <node expr="@noStack" />
                        <node expr="@visibleFilterSchema" />
                        <node expr="@visibleFilterExpr" />
                        <node expr="[folder/@fullName]" />
                        <node expr="[folder/@label]" />
                        <node expr="[folder/@id]" />
                        <node expr="[folder/parent/@fullName]" />
                        <node expr="[folder/parent/@model]" />
                        <node expr="[folder/parent/@id]" />
                    </select>
                    <where>
                        <condition enabledIf=""
                            expr="(@schema = 'xtk:schema' OR @sqlTable = 'XtkEntity') AND (@shared = true OR [@createdBy-id] = 1059)" />
                    </where>
                    <orderBy>
                        <node expr="[folder/parent/@fullName]" />
                        <node expr="[folder/@order]" />
                        <node expr="@label" />
                    </orderBy>
                </queryDef>
            </entity>
        </ExecuteQuery>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

- Response

```xml
<?xml version='1.0'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
    xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:xtk:folder'
    xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
        <LoadChildrenWithPathResponse xmlns='urn:xtk:folder'
            SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
            <pdomResult xsi:type='ns:Element'
                SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
                <folder xtkschema="xtk:folder">
                    <folder childcount="6" entity="" fullName="/Administration/" id="1006"
                        image-name="admin.png" image-namespace="xtk" isView="0"
                        label="Administration" model="xtkFolder" name="xtkAdministration" order="8"
                        parent-id="0">
                        <where filteringSchema="" />
                        <folder childcount="5" entity=""
                            fullName="/Administration/Access Management/" id="1007"
                            image-name="access.png" image-namespace="xtk" isView="0"
                            label="Access Management" model="xtkFolder" name="xtkAccess" order="10"
                            parent-id="1006">
                            <where filteringSchema="" />
                        </folder>
                        <folder childcount="2" entity="" fullName="/Administration/Audit/" id="1011"
                            image-name="" image-namespace="xtk" isView="0" label="Audit"
                            model="xtkFolder" name="xtkAudit" order="20" parent-id="1006">
                            <where filteringSchema="" />
                        </folder>
                        <folder childcount="17" entity="" fullName="/Administration/Configuration/"
                            id="1013" image-name="parameters.png" image-namespace="xtk" isView="0"
                            label="Configuration" model="xtkFolder" name="xtkParameters" order="30"
                            parent-id="1006" sort="true">
                            <data>&lt;?xml version='1.0'?&gt;
                                &lt;folder sort="true"/&gt;</data>
                            <where filteringSchema="" />
                            <folder childcount="0" entity=""
                                fullName="/Administration/Configuration/Cubes/" id="1039"
                                image-name="olapCube.png" image-namespace="xtk" isView="0"
                                label="Cubes" model="xtkOlapCube" name="xtkOlapCube" order="165"
                                parent-id="1013" schema="xtk:olapCube">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:olapCube"/&gt;</data>
                                <where filteringSchema="xtk:olapCube" />
                            </folder>
                            <folder childcount="0" entity=""
                                fullName="/Administration/Configuration/Data schemas/" id="1018"
                                image-name="schema.png" image-namespace="xtk" isView="0"
                                label="Data schemas" model="xtkSrcSchema" name="xtkSrcSchema"
                                order="30" parent-id="1013" schema="xtk:srcSchema">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:srcSchema"/&gt;</data>
                                <where filteringSchema="xtk:srcSchema" />
                            </folder>
                            <folder childcount="1" entity=""
                                fullName="/Administration/Configuration/Dynamic JavaScript pages/"
                                id="1027" image-name="script.png" image-namespace="xtk" isView="0"
                                label="Dynamic JavaScript pages" model="xtkJSSP" name="xtkJSSP"
                                order="120" parent-id="1013" schema="xtk:jssp">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:jssp"/&gt;</data>
                                <where filteringSchema="xtk:jssp" />
                            </folder>
                            <folder childcount="0" entity=""
                                fullName="/Administration/Configuration/Form rendering/" id="1029"
                                image-name="formrendering.png" image-namespace="xtk" isView="0"
                                label="Form rendering" model="xtkFormRendering"
                                name="xtkFormRendering" order="150" parent-id="1013"
                                schema="xtk:formRendering">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:formRendering"/&gt;</data>
                                <where filteringSchema="xtk:formRendering" />
                            </folder>
                            <folder childcount="2" entity=""
                                fullName="/Administration/Configuration/Global dictionary/"
                                id="1041" image-name="dictionary.png" image-namespace="xtk"
                                isView="1" label="Global dictionary" model="xtkDictionary"
                                name="xtkGlobalDictionary" order="140" parent-id="1013"
                                schema="xtk:dictionaryString">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:dictionaryString"/&gt;</data>
                                <where filteringSchema="xtk:dictionaryString" />
                            </folder>
                            <folder childcount="0" entity=""
                                fullName="/Administration/Configuration/Images/" id="1020"
                                image-name="imgfolder.png" image-namespace="xtk" isView="0"
                                label="Images" model="xtkImage" name="xtkImage" order="50"
                                parent-id="1013" schema="xtk:image">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:image"/&gt;</data>
                                <where filteringSchema="xtk:image" />
                            </folder>
                            <folder childcount="0" entity=""
                                fullName="/Administration/Configuration/Input forms/" id="1019"
                                image-name="form.png" image-namespace="xtk" isView="0"
                                label="Input forms" model="xtkForm" name="xtkForm" order="40"
                                parent-id="1013" schema="xtk:form">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:form"/&gt;</data>
                                <where filteringSchema="xtk:form" />
                            </folder>
                            <folder childcount="1" entity=""
                                fullName="/Administration/Configuration/JavaScript codes/" id="1024"
                                image-name="javascript.png" image-namespace="xtk" isView="0"
                                label="JavaScript codes" model="xtkJavascript" name="xtkJavascript"
                                order="90" parent-id="1013" schema="xtk:javascript">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:javascript"/&gt;</data>
                                <where filteringSchema="xtk:javascript" />
                            </folder>
                            <folder childcount="0" entity=""
                                fullName="/Administration/Configuration/JavaScript templates/"
                                id="1023" image-name="jst.png" image-namespace="xtk" isView="0"
                                label="JavaScript templates" model="xtkJst" name="xtkJst" order="80"
                                parent-id="1013" schema="xtk:jst">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:jst"/&gt;</data>
                                <where filteringSchema="xtk:jst" />
                            </folder>
                            <folder childcount="0" entity=""
                                fullName="/Administration/Configuration/Navigation hierarchies/"
                                id="1021" image-name="navtree.png" image-namespace="xtk" isView="0"
                                label="Navigation hierarchies" model="xtkNavTree" name="xtkNavTree"
                                order="60" parent-id="1013" schema="xtk:navtree">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:navtree"/&gt;</data>
                                <where filteringSchema="xtk:navtree" />
                            </folder>
                            <folder childcount="4" entity=""
                                fullName="/Administration/Configuration/Package management/"
                                id="1014" image-name="installedPackage.png" image-namespace="xtk"
                                isView="0" label="Package management" model="xtkFolder"
                                name="xtkPackageManagement" order="10" parent-id="1013">
                                <where filteringSchema="" />
                                <folder childcount="0" entity=""
                                    fullName="/Administration/Configuration/Package management/Package installation/"
                                    id="1015" image-name="installedPackage.png"
                                    image-namespace="xtk" isView="0" label="Package installation"
                                    model="xtkPackageInstall" name="xtkPackageInstall" order="10"
                                    parent-id="1014" schema="xtk:packageInstall">
                                    <data>&lt;?xml version='1.0'?&gt;
                                        &lt;folder schema="xtk:packageInstall"/&gt;</data>
                                    <where filteringSchema="xtk:packageInstall" />
                                </folder>
                                <folder childcount="0" entity=""
                                    fullName="/Administration/Configuration/Package management/Installed packages/"
                                    id="1016" image-name="installedPackage.png"
                                    image-namespace="xtk" isView="0" label="Installed packages"
                                    model="xtkPackage" name="xtkPackage" order="20" parent-id="1014"
                                    schema="xtk:package">
                                    <data>&lt;?xml version='1.0'?&gt;
                                        &lt;folder schema="xtk:package"/&gt;</data>
                                    <where filteringSchema="xtk:package" />
                                </folder>
                                <folder childcount="0" entity=""
                                    fullName="/Administration/Configuration/Package management/Package definitions/"
                                    id="1038" image-name="specfile.png" image-namespace="xtk"
                                    isView="0" label="Package definitions" model="xtkSpecFile"
                                    name="xtkSpecFile" order="30" parent-id="1014"
                                    schema="xtk:specFile">
                                    <data>&lt;?xml version='1.0'?&gt;
                                        &lt;folder schema="xtk:specFile"/&gt;</data>
                                    <where filteringSchema="xtk:specFile" />
                                </folder>
                                <folder childcount="0" entity=""
                                    fullName="/Administration/Configuration/Package management/Edit conflicts/"
                                    id="1017" image-name="conflict.png" image-namespace="xtk"
                                    isView="0" label="Edit conflicts" model="xtkConflict"
                                    name="xtkConflict" order="40" parent-id="1014"
                                    schema="xtk:conflict">
                                    <data>&lt;?xml version='1.0'?&gt;
                                        &lt;folder schema="xtk:conflict"/&gt;</data>
                                    <where filteringSchema="xtk:conflict" />
                                </folder>
                            </folder>
                            <folder childcount="0" entity=""
                                fullName="/Administration/Configuration/Predefined filters/"
                                id="1025" image-name="filter.png" image-namespace="xtk" isView="0"
                                label="Predefined filters" model="xtkQueryFilter"
                                name="xtkQueryFilter" order="100" parent-id="1013"
                                schema="xtk:queryFilter">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:queryFilter"/&gt;</data>
                                <where filteringSchema="xtk:queryFilter" />
                            </folder>
                            <folder childcount="1" entity=""
                                fullName="/Administration/Configuration/Reports/" id="1031"
                                image-name="report.png" image-namespace="xtk" isView="0"
                                label="Reports" model="xtkReport" name="xtkReport" order="170"
                                parent-id="1013" schema="xtk:report">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:report"/&gt;</data>
                                <where filteringSchema="xtk:report" />
                            </folder>
                            <folder childcount="0" entity=""
                                fullName="/Administration/Configuration/SQL scripts/" id="1026"
                                image-name="sql.png" image-namespace="xtk" isView="0"
                                label="SQL scripts" model="xtkSql" name="xtkSql" order="110"
                                parent-id="1013" schema="xtk:sql">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:sql"/&gt;</data>
                                <where filteringSchema="xtk:sql" />
                            </folder>
                            <folder childcount="0" entity=""
                                fullName="/Administration/Configuration/String groups/" id="1028"
                                image-name="comment.png" image-namespace="xtk" isView="0"
                                label="String groups" model="xtkStrings" name="xtkStrings"
                                order="130" parent-id="1013" schema="xtk:strings">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:strings"/&gt;</data>
                                <where filteringSchema="xtk:strings" />
                            </folder>
                            <folder childcount="0" entity=""
                                fullName="/Administration/Configuration/Web applications/" id="1030"
                                image-name="webApp.png" image-namespace="nms" isView="0"
                                label="Web applications" model="nmsWebApp" name="nmsTechnicalWebApp"
                                order="160" parent-id="1013" schema="nms:webApp">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="nms:webApp"/&gt;</data>
                                <where filteringSchema="nms:webApp" />
                            </folder>
                            <folder childcount="0" entity=""
                                fullName="/Administration/Configuration/XSL style sheets/" id="1022"
                                image-name="xslt.png" image-namespace="xtk" isView="0"
                                label="XSL style sheets" model="xtkXslt" name="xtkStylesheet"
                                order="70" parent-id="1013" schema="xtk:xslt">
                                <data>&lt;?xml version='1.0'?&gt;
                                    &lt;folder schema="xtk:xslt"/&gt;</data>
                                <where filteringSchema="xtk:xslt" />
                            </folder>
                        </folder>
                        <folder childcount="7" entity=""
                            fullName="/Administration/Campaign Management/" id="1157"
                            image-name="campaign.png" image-namespace="nms" isView="0"
                            label="Campaign Management" model="xtkFolder" name="nmsCampaignAdmin"
                            order="40" parent-id="1006">
                            <where filteringSchema="" />
                        </folder>
                        <folder childcount="6" entity="" fullName="/Administration/Platform/"
                            id="1033" image-name="extAccount.png" image-namespace="nms" isView="0"
                            label="Platform" model="xtkFolder" name="xtkPlatformAdmin" order="50"
                            parent-id="1006">
                            <where filteringSchema="" />
                        </folder>
                        <folder childcount="3" entity="" fullName="/Administration/Production/"
                            id="1167" image-name="execute.png" image-namespace="xtk" isView="0"
                            label="Production" model="xtkFolder" name="nmsProduction" order="70"
                            parent-id="1006">
                            <where filteringSchema="" />
                        </folder>
                    </folder>
                    <folder childcount="4" entity="" fullName="/Resources/" id="1178"
                        image-name="resourcePlan.png" image-namespace="nms" isView="0"
                        label="Resources" model="xtkFolder" name="nmsResources" order="9"
                        parent-id="0">
                        <where filteringSchema="" />
                    </folder>
                    <folder childcount="7" entity="" fullName="/Profiles and Targets/" id="1191"
                        image-name="usergrp.png" image-namespace="nms" isView="0"
                        label="Profiles and Targets" model="xtkFolder" name="nmsProfil" order="10"
                        parent-id="0">
                        <where filteringSchema="" />
                    </folder>
                    <folder childcount="3" entity="" fullName="/Campaign Management/" id="1199"
                        image-name="campaign.png" image-namespace="nms" isView="0"
                        label="Campaign Management" model="xtkFolder" name="nmsCampaignMgt"
                        order="11" parent-id="0">
                        <where filteringSchema="" />
                    </folder>
                    <folder childcount="20" entity="xtk:folder" fullName="/Unofficial ACC Views/"
                        id="4404" image-name="folder.png" image-namespace="xtk" isView="0"
                        label="Unofficial ACC Views" model="xtkFolder" name="unofficialAccViews"
                        order="11" parent-id="0" sort="true">
                        <data>&lt;?xml version='1.0'?&gt;
                            &lt;folder sort="true"/&gt;</data>
                        <where filteringSchema="" />
                    </folder>
                    <folder childcount="1" entity="" fullName="/Offers - design/" id="1980"
                        image-name="offerMgt.png" image-namespace="nms" isView="0"
                        label="Offers - design" model="xtkFolder" name="nmsOfferMgt" order="12"
                        parent-id="0">
                        <where filteringSchema="" />
                    </folder>
                    <folder childcount="1" entity="" fullName="/Offers - live/" id="1981"
                        image-name="offerMgt.png" image-namespace="nms" isView="0"
                        label="Offers - live" model="xtkFolder" name="nmsOfferMgtProd" order="13"
                        parent-id="0">
                        <where filteringSchema="" />
                    </folder>
                    <folder childcount="3" entity="xtk:folder" fullName="/Unofficial ACC Packages/"
                        id="3581" image-name="folder.png" image-namespace="xtk" isView="0"
                        label="Unofficial ACC Packages" model="xtkFolder"
                        name="unofficialaccPackages" order="17" parent-id="0" sort="true">
                        <data>&lt;?xml version='1.0'?&gt;
                            &lt;folder sort="true"/&gt;</data>
                        <where filteringSchema="" />
                    </folder>
                    <folder childcount="3" entity="" fullName="/Message Center/" id="5121"
                        image-name="mc.png" image-namespace="nms" isView="0" label="Message Center"
                        model="xtkFolder" name="nmsMc" order="100" parent-id="0">
                        <where filteringSchema="" />
                    </folder>
                </folder>
            </pdomResult>
        </LoadChildrenWithPathResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## Get x

- POST xx with `SOAPAction: xtk:queryDef#ExecuteQuery`

```xml
<?xml version='1.0'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
    xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:xtk:queryDef'
    xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
        <ExecuteQuery xmlns='urn:xtk:queryDef'
            SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
            <__sessiontoken xsi:type='xsd:string'></__sessiontoken>
            <entity xsi:type='ns:Element'
                SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
                <queryDef firstRows="true" ignoreDeleteStatus="false" lineCount="200"
                    operation="select" schema="xtk:specFile" startLine="0" startPath="/"
                    xtkschema="xtk:queryDef">
                    <select>
                        <node colSize="36" expr="@label" />
                        <node colSize="20" expr="@namespace" />
                        <node colSize="20" expr="@name" />
                    </select>
                    <sysFilter name="userFilter" />
                </queryDef>
            </entity>
        </ExecuteQuery>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## Get x

- POST xx with `SOAPAction: xtk:session#GetOption`

```xml
<?xml version='1.0'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
    xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:xtk:session'
    xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
        <GetOption xmlns='urn:xtk:session'
            SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
            <__sessiontoken xsi:type='xsd:string'></__sessiontoken>
            <strName xsi:type='xsd:string'>XtkSecurity_Restrict_EditXML</strName>
        </GetOption>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```
