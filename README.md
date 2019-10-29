# consulta select
```php

static function obtener_listado($db, $empresa_id, $tipo_id) {
    return $db->get("
      SELECT
        T.*
      FROM tipo T
      WHERE T.empresa_id = :empresa_id AND T.deleted IS NULL AND T.tipo_id = :tipo_id
      ORDER BY T.rotulo", false, null, array(
      'empresa_id' => $empresa_id,
      'tipo_id'    => $tipo_id,
    ));
  }


```


# consulta select con paginacion

```php

  static function obtener_oportunidades_archivados($db, $empresa_id, $oportunidad, $e) {
    return Doris::g($db)->pagination("
     SELECT
        N.id,
        N.empresa_id,
        N.contacto_id,
        CONCAT_WS(' ', P.nombres, P.apellido_paterno, P.apellido_materno) as contacto
      FROM negocio N
        JOIN tipo T1 ON T1.id = N.etiqueta_id
        JOIN tipo T2 ON T2.id = N.categoria_id
        JOIN tipo T3 ON T3.id = N.prioridad_id
        JOIN contacto C ON C.id = N.contacto_id
        JOIN persona P ON P.id = C.persona_id
      WHERE  N.deleted IS NOT  NULL AND N.empresa_id = :empresa_id AND N.oportunidad = :oportunidad" , $e ,

  array(
      'empresa_id' => $empresa_id,
      'oportunidad' => $oportunidad,
    ) );
  }




```

# INSERCION

```php
$db->insert('TABLANAME', $data );


```
# ACTUALIZACION DE TABLA

```php
$db->update('tablename', array('deleted' =>NULL), 'id ='.$n['id']);

```

# INSERT_UPDATE

esta funcion lo usamos cuando queremos insertar un dato nuevo
pero si ya existe actualizarlo

```php
$db->insert_update('tabla', $data, 'id = ' . $id);

```


# ELIMINACION LOGICA

```php

$db->deleteLogic('TABLANAME', 'id = ' . $n['id']);

```


