
using UnityEngine;

public class MoedaVR : MonoBehaviour
{
    public float tempoParaColetar = 2f;

    private float tempoOlhando = 0f;
    private bool coletada = false;

    void Update()
    {
        if (coletada) return;

        Camera cameraVR = Camera.main;
        if (cameraVR == null) return;

        Ray raio = new Ray(
            cameraVR.transform.position,
            cameraVR.transform.forward
        );

        RaycastHit hit;

        if (Physics.Raycast(raio, out hit, 20f))
        {
            if (hit.transform == transform)
            {
                tempoOlhando += Time.deltaTime;

                if (tempoOlhando >= tempoParaColetar)
                {
                    coletada = true;
                    Debug.Log("Moeda coletada!");
                    Destroy(gameObject);
                }
            }
            else
            {
                tempoOlhando = 0f;
            }
        }
        else
        {
            tempoOlhando = 0f;
        }
    }
}
