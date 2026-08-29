{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyN77PDswVLpfW/2H5mldl/N",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/kowshik5063/CSA6301-Threat-Intelligence/blob/main/Experiment%209.md\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "\n",
        "rules = [\n",
        "    {\"action\": \"ALLOW\", \"ip\": \"10.0.0.5\", \"port\": 443},\n",
        "    {\"action\": \"ALLOW\", \"ip\": \"10.0.0.5\", \"port\": 80},\n",
        "    {\"action\": \"DENY\", \"ip\": \"203.0.113.99\", \"port\": None},\n",
        "    {\"action\": \"DENY\", \"ip\": None, \"port\": 23}\n",
        "]\n",
        "\n",
        "def check_packet(ip, port):\n",
        "    for rule in rules:\n",
        "        ip_match = rule[\"ip\"] in (None, ip)\n",
        "        port_match = rule[\"port\"] in (None, port)\n",
        "\n",
        "        if ip_match and port_match:\n",
        "            return rule[\"action\"]\n",
        "\n",
        "    return \"DENY\"\n",
        "\n",
        "packets = [\n",
        "    (\"10.0.0.5\", 443),\n",
        "    (\"203.0.113.99\", 80),\n",
        "    (\"10.0.0.9\", 23),\n",
        "    (\"10.0.0.9\", 8080)\n",
        "]\n",
        "\n",
        "for ip, port in packets:\n",
        "    decision = check_packet(ip, port)\n",
        "    print(f\"Packet from {ip}:{port} -> {decision}\")"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "T70NqXbe-FlL",
        "outputId": "3890003a-3c83-4487-ae3b-5aa8d4098864"
      },
      "execution_count": 3,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Packet from 10.0.0.5:443 -> ALLOW\n",
            "Packet from 203.0.113.99:80 -> DENY\n",
            "Packet from 10.0.0.9:23 -> DENY\n",
            "Packet from 10.0.0.9:8080 -> DENY\n"
          ]
        }
      ]
    }
  ]
}