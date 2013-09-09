===============================
Ordinare un CActiveDataProvider
===============================

--------
Scenario
--------

::

    $sort = new CSort();
    $sort->attributes = array(
        'da_data',
        'a_data',
        'totale_giorni_assenza' => array(
            'asc'=>'a_data - da_data',
            'desc'=>'a_data - da_data desc'
         ),
    );

    $this->ferie_provider = new CActiveDataProvider('FerieGiorni',array(
        'criteria'=>array(
            'condition'=>'iddipendente = ' .$this->dipendente->oid,
        ),
        'sort'=>$sort,
        'pagination'=>array(
            'pageSize'=>6,
        ),
    ));