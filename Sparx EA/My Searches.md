

# My Searches

Sparx Enterprise Architect (EA) includes a model search feature. This includes the ability to [save your own searches (My Searches)][1] for future reference.

The sections below are example searches that could be of used to Sparx EA users. They have been split into two groupings:
* Reusable Searches - examples usable without modification
* Project Examples - project examples that may require some modification

The searches can be installed by pasting the SQL block into the "SQL Editor" within the model search feature. These can be saved for future use.

Tips for creating your own searches:
* Use the scratchpad's autocomplete feature to find column names within a table. e.g. enter "t_connector." to see a list of columns within the table
* Use "\<Search Term\>" within the SQL block whereever you want the search term to be replaced
* Selecting "ea_guid AS CLASSGUID" allows you to open the properties of a search result directly, and to find it on diagrams, via the search result's context menu

## Warning: Searches can be repository type specific 

When using wildcard search parameters you [may need to vary the wildcards based upon your repository type][2]. e.g. For local EAP files the asterix (\*) should find any set of characters, but when using this same search against an SQL Server based repository you will need to replace your asterix wildcards with percent (\%) wildcards characters.

e.g. the "Component Flows (by Source/Sink)" search below was developed for a shared repository, and this line:
```
	   and (o2.Name like '%<Search Term>%' or o3.Name like '%<Search Term>%')
```
may need to be replaced by this line
```
	   and (o2.Name like '*<Search Term>*' or o3.Name like '*<Search Term>*')
```
to work in a local EAP file.

# Reusable Searches

## Component Flows (by Source/Sink)

Searches for Information Flow relationships between UML components. The search term is used to restrict the sink/source components.

```
select 
       c1.ea_guid AS CLASSGUID, 
       c1.Connector_Type AS CLASSTYPE, 
       't_connector' as CLASSTABLE,
       c1.Name as "FlowName",
       c1.styleex as "FlowAlias",
       c1.Stereotype as "FlowStereotype",
	   c1.Connector_Type as "FlowType",
       o2.Name as "FlowSource",
       o3.Name as "FlowSink",
       '"' + c1.Notes + '"' as "FlowNotes",
       o2.object_type as "SourceObjectType",
       o3.object_type as "SinkObjectType",
       c1.connector_id as "FlowConnectorID",
       o2.object_id as "SourceObjectId",
       o3.object_id as "SinkObjectId"

       
from t_connector c1, t_object o2, t_object o3
where 
           (c1.Connector_Type = 'InformationFlow')
       and (o2.Object_ID = c1.start_object_id) 
       and (o3.Object_ID = c1.end_object_id) 
	   and (o2.Name like '%<Search Term>%' or o3.Name like '%<Search Term>%')
	   and (o2.object_type = 'Component' and o3.object_type = 'Component')
```

## Object Flows (by Name)


Searches for Information Flow relationships between elements. The search term is used to restrict the relationships by name.

```
select 
	   c1.ea_guid AS CLASSGUID, 
	   c1.Connector_Type AS CLASSTYPE, 
	   't_connector' as CLASSTABLE,
       c1.Name as "FlowName",
       c1.styleex as "FlowAlias",
       c1.Stereotype as "FlowStereotype",
	   c1.Connector_Type as "FlowType",
       o2.Name as "FlowSource",
       o3.Name as "FlowSink",
       '"' + c1.Notes + '"' as "FlowNotes",
       c1.connector_id as "FlowConnectorID",
       o2.object_id as "SourceObjectId",
       o3.object_id as "SinkObjectId"

       
from t_connector c1, t_object o2, t_object o3
where 
           (c1.Connector_Type = 'InformationFlow')
	   and (c1.Name like '%<Search Term>%')
       and (o2.Object_ID = c1.start_object_id) 
       and (o3.Object_ID = c1.end_object_id) 
```

## Object Flows (by Source/Sink)

Searches for Information Flow relationships between elements. The search term is used to restrict the sink/source elements.

```
select 
       c1.ea_guid AS CLASSGUID, 
       c1.Connector_Type AS CLASSTYPE, 
       't_connector' as CLASSTABLE,
       c1.Name as "FlowName",
       c1.styleex as "FlowAlias",
       c1.Stereotype as "FlowStereotype",
	   c1.Connector_Type as "FlowType",
       o2.Name as "FlowSource",
       o3.Name as "FlowSink",
       '"' + c1.Notes + '"' as "FlowNotes",
       o2.object_type as "SourceObjectType",
       o3.object_type as "SinkObjectType",
       c1.connector_id as "FlowConnectorID",
       o2.object_id as "SourceObjectId",
       o3.object_id as "SinkObjectId"

       
from t_connector c1, t_object o2, t_object o3
where 
           (c1.Connector_Type = 'InformationFlow')
       and (o2.Object_ID = c1.start_object_id) 
       and (o3.Object_ID = c1.end_object_id) 
	   and (o2.Name like '%<Search Term>%' or o3.Name like '%<Search Term>%')
	   and not(o2.object_type = 'UMLDiagram' or o3.object_type = 'UMLDiagram')
```

## Flows

```
select 
       t_package.Name as "PackageName",
       o1.Name as "ObjectName",
       o1.ModifiedDate as "ObjectModifiedDate",
       o1.CreatedDate as "ObjectCreatedDate",
       c1.Name as "FlowName",
       c1.styleex as "FlowAlias",
       o2.Name as "FlowSource",
       o3.Name as "FlowSink",
       '"' + c1.Notes + '"' as "FlowNotes",
       o1.Object_id as "ObjectID",
       c1.connector_id as "FlowConnectorID",
       o2.object_id as "SourceObjectId",
       o3.object_id as "SinkObjectId",
       proxyo1.object_id as "ProxyConnectorObjectId",
       proxyc1.connector_id as "ProxyConnectorConnectionId"
       
from t_object o1, t_package, t_connector c1, t_object proxyo1, t_connector proxyc1, t_object o2, t_object o3
where 
(o1.Package_ID = t_package.Package_ID)
       and (o2.Object_ID = c1.start_object_id) 
       and (o3.Object_ID = c1.end_object_id)
       and (proxyc1.end_object_id = o1.object_id) 
       and (proxyc1.start_object_id = proxyo1.object_id)
       and (proxyo1.classifier = c1.connector_id)
       
order by
       t_package.Name, o1.name;
```

# Project Examples

The following examples are sourced from project models and make use of stereotypes or naming schemes specific to those models. They will require some modification before reuse in another context.

## Diagram Contents (SUC and INT)

Searches for elements displayed on diagrams, where the diagrams are named using predefined naming schemes.

```
select 
       d.diagram_id as diagram_id,
       '"' + d.name  + '"' as diagram_name,
       d.stereotype as diagram_stereotype,
       o.object_id as object_id, 
       '"' + o.name + '"' as object_name,
       o.object_type,
       o.alias as object_alias,
       o.stereotype as object_stereotype
       
from 
t_diagram d, t_diagramobjects d2, t_object o

where 
(d.name like '%-SUC-%' OR d.name like '% INT%')
and d.Diagram_ID = d2.Diagram_ID
and d2.Object_ID = o.Object_ID
;
```

## Relationships (with Associated Element)

Searches for relationships between model elements, where the relationship has an element with a specific stereotype associated to the relationship.

```
select 
       t_package.Name as "SubjectArea",
       o1.Name as "ConceptName",
       o1.ModifiedDate as "ConceptModifiedDate",
       o1.CreatedDate as "ConceptCreatedDate",
       c1.Name as "FlowName",
       c1.styleex as "FlowAlias",
       o2.Name as "FlowSource",
       o3.Name as "FlowSink",
       '"' + c1.Notes + '"' as "FlowNotes",
       o1.Object_id as "ConceptObjectID",
       c1.connector_id as "FlowConnectorID",
       o2.object_id as "SourceObjectId",
       o3.object_id as "SinkObjectId",
       proxyo1.object_id as "ProxyConnectorObjectId",
       proxyc1.connector_id as "ProxyConnectorConnectionId"
       
from t_object o1, t_package, t_connector c1, t_object proxyo1, t_connector proxyc1, t_object o2, t_object o3
where 
              (o1.Stereotype = 'CDM_entity')
       and (o1.Package_ID = t_package.Package_ID)
       and (o2.Object_ID = c1.start_object_id) 
       and (o3.Object_ID = c1.end_object_id)
       and (proxyc1.end_object_id = o1.object_id) 
       and (proxyc1.start_object_id = proxyo1.object_id)
       and (proxyo1.classifier = c1.connector_id)
       
order by
       t_package.Name, o1.name;
```

[1]: https://sparxsystems.com/enterprise_architect_user_guide/14.0/model_navigation/creating_filters.html
[2]: https://www.sparxsystems.com/forums/smf/index.php?topic=38387.0
