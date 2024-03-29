.. index:: pair: page; Convert a PyTorch F3Net Model
.. _conv_prep__pytorch_f3_net:

.. meta::
   :description: This tutorial demonstrates how to convert a F3Net model
                 from Pytorch to the OpenVINO Intermediate Representation.
   :keywords: Model Optimizer, tutorial, convert a model, model conversion, 
              --input_model, --input_model parameter, command-line parameter, 
              OpenVINO™ toolkit, deep learning inference, OpenVINO Intermediate 
              Representation, Pytorch, F3Net, F3Net model, pre-trained model, 
              convert a model to OpenVINO IR

Convert a PyTorch F3Net Model
=============================

:target:`conv_prep__pytorch_f3_net_1md_openvino_docs_mo_dg_prepare_model_convert_model_pytorch_specific_convert_f3net` `F3Net <https://github.com/weijun88/F3Net>`__ : Fusion, Feedback and Focus for Salient Object Detection

Clone the F3Net Repository
~~~~~~~~~~~~~~~~~~~~~~~~~~

To clone the repository, run the following command:

.. ref-code-block:: cpp

   git clone http://github.com/weijun88/F3Net.git

Download and Convert the Model to ONNX
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To download the pre-trained model or train the model yourself, refer to the `instructions <https://github.com/weijun88/F3Net/blob/master/README.md>`__ in the F3Net model repository. First, convert the model to ONNX format. Create and run the following Python script in the ``src`` directory of the model repository:

.. ref-code-block:: cpp

   import torch
   from dataset import Config
   from net import F3Net

   cfg = Config(mode='test', snapshot=<path_to_checkpoint_dir>)
   net = F3Net(cfg)
   image = torch.zeros([1, 3, 352, 352])
   torch.onnx.export(net, image, 'f3net.onnx', export_params=True, do_constant_folding=True, opset_version=11)

The script generates the ONNX model file ``f3net.onnx``. The model conversion was tested with the commit-SHA: ``eecace3adf1e8946b571a4f4397681252f9dc1b8``.

Convert an ONNX F3Net Model to IR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. ref-code-block:: cpp

   mo --input_model <MODEL_DIR>/f3net.onnx

