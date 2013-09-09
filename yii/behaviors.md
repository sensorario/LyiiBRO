=========
Behaviors
=========

--------
Scenario
--------

La tipica situazione in cui si incorre nella necessità di avere un behavior per le mani, è quando bisogna mostrare un campo data. In particolare le date vengono salvate nel formato yyyy-mm-dd hh:ii:ss ma noi, per esempio, vogliamo visualizzarle nel formato dd/mm/yyyy. Che fare?

------------------------
Una possibile soluzione:
------------------------

Un behavior è una classe i cui metodi possono essere importati attaccandoli ad un altro componente. Il problema delle date può ripetersi in più classi e siccome php non supporta l'ereditarietà multipla, il behavior può dare ai model che ne hanno bisogno un comportamento in più. In questo behavior vi mostro come creare un semplice behavior che mostra un dato nel modo che preferiamo.

Per prima cosa dobbiamo aggiungere il behavior alla classe che ne ha bisogno. Per farlo indicheremo semplicemente il nome della classe che implementa il nostro behavior e se necessario potremo impostare degli attributo di questa classe. Nel nostro caso, indicheremo il nome del campo oggetto del nostro behavior. Abbiamo indicato come campo 'field' perché SensorarioDateTimeBehavior ha un attributo pubblico con questo nome.

::

    public function behaviors() {
        return array('sensorario-date-time' => array(
                'class' => 'application.components.SensorarioDateTimeBehavior',
                'field' => 'data'
        ));
    }

In secondo luogo, il nostro behavior può essere implementato in questo modo:

::

    class SensorarioDateTimeBehavior extends CActiveRecordBehavior {

        public $field;

        public function afterFind($event) {
            $array = array();
            if (preg_match("/([0-9]{1,4})-([0-9]{1,2})-([0-9]{2,4})/", $this->owner->{$this->field}, $array)) {
                $this->owner->{$this->field} = "{$array[3]}/{$array[2]}/{$array[1]}";
            }
            return parent::afterFind($event);
        }

    }