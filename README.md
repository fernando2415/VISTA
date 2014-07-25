VISTA
=====
USE VENTASCIB

SELECT DF.NUM_FAC,P.COD_PRO,P.DES_PRO
   FROM TB_DETALLE_FACTURA DF INNER JOIN TB_PRODUCTO P
   ON DF.COD_PRO=P.COD_PRO

   SELECT NUM_FAC,COUNT(COD_PRO) AS CAN_PRO
   FROM TB_DETALLE_FACTURA
   GROUP BY NUM_FAC

   ------- REALICE UNA CONSULTA QUE LISTE EL COD_PRO DES_PRO Y LA SUMA TOTAL VENDIDA DE DICHO PRODUCTO
   

   CREATE VIEW V_TOTALPRODUCTO
   AS
   SELECT P.COD_PRO, P.DES_PRO,SUM (CAN_VEN) AS TOTAL_VEN
     FROM TB_PRODUCTO P INNER JOIN TB_DETALLE_FACTURA DF
	 ON P.COD_PRO=DF.COD_PRO 
	 GROUP BY P.COD_PRO,P.DES_PRO HAVING SUM (CAN_VEN)>100

	 SELECT * FROM V_TOTALPRODUCTO WHERE TOTAL_VEN>100



	------- REALICE UNA CONSULTA QUE LISTE COD_VEN NOM_VEN APE_VEN Y CANTIDAD DE CLIENTES A LOS CUALES HA FACTURADO

	 CREATE VIEW V_TOTALCLIENTE_VEN
	 AS
	 SELECT V.COD_VEN, V.NOM_VEN, V.APE_VEN ,COUNT(COD_CLI) AS CANT_CLI
	 FROM TB_VENDEDOR V INNER JOIN TB_FACTURA F
	 ON V.COD_VEN=F.COD_VEN
	 GROUP BY V.COD_VEN, V.NOM_VEN, V.APE_VEN

	 SELECT * FROM V_TOTALCLIENTE_VEN

