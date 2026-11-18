<?php
class Carga {
    private $idCarga;
    private $destino;
    private $volume;
    private $disponivel;

    public function __construct($idCarga, $destino, $volume, $disponivel) {
        $this->idCarga = $idCarga;
        $this->destino = $destino;
        $this->volume = $volume;
        $this->disponivel = $disponivel;
    }

    public static function findAllDisponivel() {
        $pdo = new PDO('sqlite:transporta.db');
        $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

        $st = $pdo->prepare('SELECT * FROM Carga WHERE disponivel = 1');
        $st->execute();

        $cargas = array();

        while ($reg = $st->fetch(PDO::FETCH_ASSOC)) {
            $cargas[] = new Carga(
                $reg['idCarga'],
                $reg['destino'],
                $reg['volume'],
                $reg['disponivel']
            );
        }

        return $cargas;
    }

    public function getIdCarga() {
        return $this->idCarga;
    }

    public function getDestino() {
        return $this->destino;
    }

    public function getVolume() {
        return $this->volume;
    }

    public function getDisponivel() {
        return $this->disponivel;
    }
}
?>